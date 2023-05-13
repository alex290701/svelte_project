<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher();

    let name;
    let role;
    let age;
    let id;

    const submithandle = () => {
        const person = {name,role,age,id};
        dispatch('add', person);
    };
</script>

<form on:submit|preventDefault={submithandle}>
    <input type="text" placeholder="Name" bind:value={name}>
    <input type="text" placeholder="Role" bind:value={role}>
    <input type="number" placeholder="Age" bind:value={age}>
    <input type="number" placeholder="ID" bind:value={id}><br>
    <button>Add</button>
</form>

<style>

</style>