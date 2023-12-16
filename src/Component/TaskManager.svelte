<script>
  import ModalForm from './ModalForm.svelte';

  let formModal = false;
  let tasks = [];

  function handleFormSubmit(event) {
    tasks = [...tasks, event.detail];
    formModal = false; // Close the modal after submission
    console.log("New Task Added:", tasks);
  }

  function deleteTask(index) {
    tasks = tasks.filter((_, i) => i !== index);
    console.log("Task deleted:", tasks);
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
    <h2>Time and Date</h2>
    <h2>Action</h2>
  </div>

  <div class="task-manager-list">
    <!-- Displaying Tasks -->
    {#each tasks as task, index}
      <div class="task-manager-list-item">
        <h2>{task.task}</h2>
        <h2>{task.assignedTo}</h2>
        <h2>{task.timeDate}</h2>
        <button on:click={() => deleteTask(index)} class="delete-task-button">Delete</button>
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
  grid-template-columns: repeat(4, 1fr); /* Create 4 equally spaced columns */
  background-color: rgb(190, 196, 203);
  margin-left: 10px;
  margin-right: 10px;
  padding: 8px; /* Add padding for spacing */
  font-weight: bold;
  }

  
  .task-manager-list{
   display: flex;
  flex-direction: column; /* Stack items vertically */
  gap: 10px;
  }

  .task-manager-list-item {
    display: grid; /* Use grid for better alignment */
  grid-template-columns: repeat(4, 1fr); /* Create 4 equally spaced columns */
  align-items: center;
  padding: 8px;
  font-weight: normal;
  border-bottom: 1px solid #ccc;
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


  /* Additional styles as needed */
</style>
