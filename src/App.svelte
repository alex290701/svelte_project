<script>
	import Modal from './Modal.svelte'
	import AddAssociates from './AddAssociateForm.svelte'

	let showmodal = false;
	let associates = [
		{name: 'Antony', role: 'Ros Developer', age: 21, id: 1},
		{name: 'Salai', role: 'Sr. Ros Developer', age: 21, id: 2},
		{name: 'Adarsh', role: 'Software Developer', age: 21, id: 3}
	];
	let name = " ";
	let age = 0;
	let role = " ";
	let id = 0;

	const update_handle = () => {
		showmodal = !showmodal;
	};
	const delete_handle = (id) => {
		associates = associates.filter((person) => person.id!=id);	
	};
	const add_handle = (e) => {
		const person = e.detail; 
		associates = [person, ...associates];
		showmodal = false;
	};
</script>

<Modal {showmodal} on:click={update_handle}>
	<AddAssociates on:add={add_handle}/>
</Modal>
<main>
<button on:click={update_handle}>Update</button>
{#each associates as person (person.id)}
	<div>
		<h4>{person.name}</h4>
		<p>
			{person.role}, {person.age} years old.
			<button on:click={()=>{delete_handle(person.id)}}>Delete</button>
		</p>
	</div>
{:else}
	<p>There are no associates to show...</p>
{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>