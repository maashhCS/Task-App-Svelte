<script lang="ts">
	let newTask = $state('');
	let {
		addTask
	}: {
		addTask: (task: string) => void;
	} = $props();

	function formSubmitted(e: SubmitEvent) {
        if (newTask.trim() === '') {
            return;
        }
        e.preventDefault();
		addTask(newTask);
        newTask = '';
	}
</script>

<form onsubmit={formSubmitted}>
	<label>
		<input name="newTask" class="rounded-sm" bind:value={newTask} placeholder="Add a new task" />
	</label>
	<div class="button-container mt-2">
		<button
			class="cursor-pointer rounded-sm px-3 py-2 shadow-sm outline outline-black/20"
			>Add</button
		>
	</div>
</form>

<style>
	.button-container {
		display: flex;
		justify-content: flex-end;
	}

	input {
		border: 1px solid #ccc;
		padding: 0.5rem;
		width: 100%;
	}

    form {
        margin-bottom: 1rem;
    }
</style>
