<script>
	import Modal from './Modal.svelte'
	import AddAssociates from './AddAssociateForm.svelte'
	import Header from './Header.svelte'
	let showmodal = false;
	let associates = [
		{name: 'Tony', role: 'Developer', age: 25, id: 15486},
		{name: 'Mark', role: 'Sr.Developer', age: 30, id: 14852},
		{name: 'Stuart', role: 'Design Engineer', age: 27, id: 18564}
	];

	let error_msg = '';
	let error = false;
	const add_handle = () => {
		showmodal = !showmodal;
	};
	const delete_handle = (id) => {
		associates = associates.filter((person) => person.id!=id);	
	};
	const update_handle = (e) => {
		const person = e.detail;
		for(var key in associates){
			if(associates[key].id === person.id){
				error = true;
				break;
			}
		}
		if(error){
			error_msg = 'Duplicate ID';
			error = false;
		}
		else{
			associates = [person, ...associates];
			showmodal = false;
		}
	};
</script>

<Modal {showmodal} on:click={add_handle}>
	<AddAssociates on:update={update_handle}>
		<div class="error">
			<p>{error_msg}</p>
		</div>
	</AddAssociates>
	
</Modal>
<Header />

<main>
<button class="update" on:click={add_handle}>Add</button>
	<div class="table">
		<table>
			<tr>
				<th>ID</th>
				<th>Name</th>
				<th>Age</th>
				<th>Role</th>
				<th></th>
			</tr>
			{#each associates as person }
				<tr>
					<td>{person.id}</td>
					<td>{person.name}</td>
					<td>{person.age}</td>
					<td>{person.role}</td>
					<td><button class="delete" on:click={() => delete_handle(person.id)}>Delete</button></td>
				</tr>
			{:else}
				<tr>
					<td colspan="5">There are no associates to display...</td>
				</tr>
			{/each}
			</table>
	</div>
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

	table {
		border-collapse: collapse;
		width: 75%;
		color:white;
		font-family: Arial, sans-serif;
		font-size: 14px;
		text-align: left;
		border-radius: 10px;
		overflow: hidden;
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
		margin: auto;
		margin-top: 50px;
		margin-bottom: 50px;
	} 
	table th {
		text-align: center;
		background-color: black;
		color: #fff;
		font-weight: bold;
		font-size: large;
		padding: 10px;
		text-transform: uppercase;
		letter-spacing: 1px;
		/* border-top: 1px solid #fff; */
		border-bottom: 1px solid #ccc;
	}
	table tr:nth-child(even) td {
		background-color: #f2f2f2;
	}

	/* table tr:hover td {
		background-color: #ffedcc;
	} */
	table td {
		background-color: #fff;
		padding: 10px;
		border-bottom: 1px solid #ccc;
		/* font-weight: bold; */
		font-size: larger;
		color: black;
		text-align: center;
	}
	.update{
		border-radius: 10px;
		box-shadow: 0 0 20px rgba(0, 0, 0, 0.4);
		background-color: rgb(15, 126, 11);
		color: white;
		border: 0;
		font-size: x-large;
		font-weight: bold;
		cursor: pointer;
		min-width: 100px;
		min-height: 50px;
	}
	.delete{
		border-radius: 10px;
		box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
		cursor: pointer;
	}
</style>