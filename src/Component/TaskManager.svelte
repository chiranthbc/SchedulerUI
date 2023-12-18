<script>
  import ModalForm from './ModalForm.svelte';

  let formModal = false;
  let tasks = [];
  let editIndex = null; // Track the index of the task being edited
  


  function handleFormSubmit(event) {
     const { task, assignedTo, timeDate } = event.detail;
      // Assuming timeDate is '2023-12-18T12:13'
      const formattedDateTime = new Date(timeDate).toLocaleString('en-US', {
        dateStyle: 'medium', // Adjust the date style as needed (long, medium, short, full)
        timeStyle: 'short', // Adjust the time style as needed (long, medium, short)
      });


   const updatedTask = {
    task,
    assignedTo,
    timeDate: formattedDateTime,
    selectedJob: '/job',
    selectedatask:'/task',
  };

    if (editIndex !== null) {
      // If editIndex is not null, update existing task
      tasks[editIndex] = updatedTask;
      editIndex = null; // Reset editIndex after editing
      console.log("Task Edited:", tasks);
    } else {
      // If editIndex is null, add a new task
      tasks = [...tasks, updatedTask];
      console.log("New Task Added:", tasks);
    }
    formModal = false; // Close the modal after submission
  }

  function deleteTask(index) {
    tasks = tasks.filter((_, i) => i !== index);
    console.log("Task deleted:", tasks);
  }

  function editTask(index) {
    // Set the editIndex and populate form with existing task details
   
    editIndex = index;
    const taskToEdit = tasks[index];
    // Open modal for editing
    formModal = true;
    // Update form values with task details for editing
    values = {
      task: taskToEdit.task,
      assignedTo: taskToEdit.assignedTo,
      timeDate: taskToEdit.timeDate
    };
  }

   function handleSelectedTask(index, event) {
    const selectedTaskValue = event.target.value;
    if (tasks[index]) {
      tasks[index].selectedTask = selectedTaskValue;
      console.log('Selected Task:', selectedTaskValue);
    }
  }

  function handleSelectedJob(index, event) {
    const selectedJobValue = event.target.value;
    if (tasks[index]) {
      tasks[index].selectedJob = selectedJobValue;
      console.log('Selected Job:', selectedJobValue);
    }
  }
</script>


<div class="task-manager">
    <div class="header">
      <h1><i class="fa-solid fa-calendar-days"></i> Task Lists</h1>
      <button on:click={() => (formModal = true)} class="add-task-button">Add New Task</button>
      <div class="modal">
        {#if formModal}
          <ModalForm on:submit={handleFormSubmit} />
        {/if}
      </div>
    </div>
    <div class="task-manager-header">
          <h2>Task</h2>
          <h2>Assigned To</h2>
          <h2>Date and Time</h2>
          <!-- <h2>Task</h2> -->
          <h2>Job</h2>
          <h2>Action</h2>
      </div>
      <div class="task-manager-list">
            <!-- Displaying Tasks -->
            {#each tasks as task, index (task)}
             <!-- Use a unique variable for each task's selection -->
             
                <div class="task-manager-list-item" key={task.task}>
                  <h2>{task.task}</h2>
                  <h2>{task.assignedTo}</h2>
                  <h2>{task.timeDate}</h2>
                  
                 

                  <div class="job-dropdown">
                      <select bind:value={task.selectedJob} id={`jobDropdown_${index}`} on:change={(event) => handleSelectedJob(index, event)} >
                        <option value="/job">Job</option>
                        <option value="/create">Create</option>
                        <option value="/search">Search</option>
                        <option value="/fetch">Fetch</option>
                        <option value="/delete">Delete</option>
                        <option value="/save">Save</option>
                        <option value="/cancel">Cancel</option>
                        <option value="/activate">Activate</option>
                      
                        <option value="/executenow">Executenow</option>
                        <option value="/setdependency">Setdependency</option>
                        <option value="/removedependency">Removedependency</option>
                        
                      </select> 
                  </div>
                   
                  <div class="task-dropdown">
                    <!-- <button on:click={() => editTask(index)} class="edit-task-button">Edit</button>
                    <button on:click={() => deleteTask(index)} class="delete-task-button">Delete</button> -->

                     <select bind:value={task.selectedTask} id={`jobDropdown_${index}`} on:change={(event) => handleSelectedTask(index, event)} >
                        <option value="/task">Task</option>
                        <option value="/create">Create</option>
                        <option value="/search">Search</option>
                        <option value="/fetch">Fetch</option>
                        <option value="/delete">Delete</option>
                        <option value="/save">Save</option>
                        <option value="/cancel">Cancel</option>
                        <option value="/activate">Activate</option>
                      
                        <option value="/executenow">Executenow</option>
                        <option value="/setdependency">Setdependency</option>
                        <option value="/removedependency">Removedependency</option>
                        
                      </select> 


                  </div>
                </div>
            {/each}
        </div>
</div>


 
<style>
  .task-manager {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    overflow: hidden;
  }

  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 20px;
    margin-right: 20px;
    margin-left: 20px;
  }

  .header h1 {
    font-weight: bold;
    font-size: 24px;
    display: flex;
    align-items: center;
  }

  .header h1 i {
    margin-right: 5px;
  }

  .add-task-button {
    background-color: black;
    color: red;
    border: 1px solid red;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    width: fit-content;
  }

  .task-manager-header {
      display: grid; /* Use grid for more precise control */
  grid-template-columns: repeat(5, 1fr); /* Create 4 equally spaced columns */
  background-color: rgb(190, 196, 203);
  margin-left: 10px;
  margin-right: 10px;
  padding: 8px; /* Add padding for spacing */
  font-weight: bold;
  font-size: 16px;
  }

  
  .task-manager-list{
   display: flex;
  flex-direction: column; /* Stack items vertically */
  gap: 10px;
  }

  .task-manager-list-item {
    display: grid; /* Use grid for better alignment */
  grid-template-columns: repeat(5, 1fr); /* Create 4 equally spaced columns */
  align-items: center;
  padding: 8px;
  font-weight: normal;
  border-bottom: 1px solid #ccc;
  font-size: 14px;
  }

 .delete-task-button {
    background-color: #ff6347;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  width: fit-content;
  transition: background-color 0.3s ease; /* Smooth transition on hover */
} 
 .edit-task-button {
    background-color: #ff6347;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  width: fit-content;
  transition: background-color 0.3s ease; /* Smooth transition on hover */
}

  .delete-task-button:hover {
    background-color: #ff7f50;
  } 
  .modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 40%;
    height: 40%;
    /* Additional styling for the modal */
    /* Define width, background, padding, etc. */
  }
  /* Style the dropdown and button as needed */
  
  .job-dropdown {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }
.task-dropdown {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }


  select {
    font-weight: bold;
    padding: 8px;
    border-radius: 4px;
    border: 2px solid #ccc;
    margin-right: 10px;
  }

  

  /* Additional styles as needed */
</style>
