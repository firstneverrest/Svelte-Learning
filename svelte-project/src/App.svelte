<script lang="ts">
	import Modal from './Modal.svelte'

	let showModal = false;

	const toggleModal = () => {
		showModal = !showModal
	}
</script>

<Modal message="Thank you for visiting our website!" {showModal} on:click={toggleModal}>
	<form>
		<input type="text" placeholder="name">
		<input type="text" placeholder="job">
		<button>Add Employee</button>
	</form>
	<div slot="title">
		<h3>Add a New Employee</h3>
	</div>
</Modal>

<main>
	<h1>This is my Application</h1>
	<button on:click={toggleModal}>Open Modal</button>
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