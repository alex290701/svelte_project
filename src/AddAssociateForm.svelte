<script>
    import { createEventDispatcher } from 'svelte';
  
    let dispatch = createEventDispatcher();
    let fields = { name: '', role: '', age: '', id:''};
    let errors = { name: '', role: '', age: '', id:'' };
    let valid = false;
  
    const submitHandler = () => {
      valid = true;
      // question
      if (fields.name.trim().length < 1) {
        valid = false;
        errors.name = 'Name can not be empty'
      } else {
        errors.name = ''
      }
      // answer A
      if (fields.role.trim().length < 1) {
        valid = false;
        errors.role = 'Role cannot be empty'
      } else {
        errors.role = ''
      }
      // answer B
      if (fields.age < 1) {
        valid = false;
        errors.age = 'Age cannot be empty'
      } else {
        errors.age = ''
      }
      if (fields.id < 1) {
        valid = false;
        errors.id = 'ID cannot be empty'
      } else {
        errors.id = ''
      }
      // add new poll
      if (valid) {
        let poll = {...fields};
        dispatch('update', poll);
      }
    }
  </script>
  
  <main>
    <form on:submit|preventDefault={submitHandler}>
        <div class="form-field">
        <label for="Name">Poll Question:</label>
        <input type="text" id="Name" bind:value={fields.name}>
        <div class="error">{ errors.name }</div>
        </div>
        <div class="form-field">
        <label for="role">Role:</label>
        <input type="text" id="role" bind:value={fields.role}>
        <div class="error">{ errors.role }</div>
        </div>
        <div class="form-field">
        <label for="age">Age:</label>
        <input type="number" id="age" bind:value={fields.age}>
        <div class="error">{ errors.age }</div>
        </div>
        <div class="form-field">
            <label for="age">ID:</label>
            <input type="number" id="ID" bind:value={fields.id}>
            <div class="error">{ errors.id }</div>
        </div>
        <button>update</button>
    </form>
    <slot></slot>
</main>
  
  <style>
    form{
      width: 400px;
      margin: 0 auto;
      text-align: center;
    }
    .form-field{
      margin: 18px auto;
    }
    input{
      width: 100%;
      border-radius: 6px;
    }
    label{
      margin: 10px auto;
      text-align: left;
    }

    button{
		border-radius: 10px;
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.4);
		background-color: rgb(15, 126, 11);
		color: white;
		border: 0;
		/* font-size: x-large; */
		font-weight: bold;
		cursor: pointer;

	}

  </style>