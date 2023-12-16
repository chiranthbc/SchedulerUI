<!-- ModalForm.svelte -->
<script>
    import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  let values = {
    task: '',
    assignedTo: '',
    timeDate: ''
  };


  function handleSubmit() {
    const formValues = { ...values };
    dispatch('submit', formValues); // Emitting the submit event with form values
    values = { task: '', assignedTo: '', timeDate: '' }; // Resetting form values
  }
  
</script>

<div class="modal-form">
  <form on:submit|preventDefault={handleSubmit}>
    <h3>New Task</h3>
    <label for="task">Task</label><br>
    <input type="text" name="task" bind:value={values.task}><br>
    <label for="assignedTo">Assigned To</label><br>
    <input type="text" name="assignedTo" bind:value={values.assignedTo}><br>
    <label for="timeDate">Time and Date</label><br>
    <input type="datetime-local" name="timeDate" bind:value={values.timeDate}><br><br>
    <button type="submit">Submit</button><br>
  </form>
</div>

<!-- ModalForm.svelte -->
<style>
  .modal-form {
    /* Styles for the form container */
    padding: 20px;
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }

  .modal-form label {
    /* Styles for form labels */
    display: block;
    margin-bottom: 5px;
  }

  .modal-form input {
    /* Styles for form inputs */
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 16px;
    box-sizing: border-box;
  }

  .modal-form button {
    /* Styles for form submit button */
    display: block;
    width: 100%;
    padding: 8px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
  }

  .modal-form button:hover {
    /* Hover styles for form submit button */
    background-color: #0056b3;
  }
  label{
    font-weight: bold;
  }
  /* Additional styles as needed */
</style>

