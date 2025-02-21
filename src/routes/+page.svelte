<script lang="ts">
	import type { Task } from '$lib/types';
	import TasksForm from '../lib/components/tasks-form.svelte';
	import TaskList from '$lib/components/task-list.svelte';

	let message = 'Tasks';
	let tasks = $state<Task[]>([]);
	let totalDone = $derived(tasks.reduce((total, task) => total + Number(task.done), 0));
	function addTask(newTask: string) {
		tasks.push({
			id: crypto.randomUUID(),
			title: newTask,
			done: false
		});
	}

	function toggleDone(task: Task) {
		task.done = !task.done;
	}

	function removeTask(id: string) {
		tasks = tasks.filter((t) => t.id !== id);
	}
</script>

<main>
	<h3>{message}</h3>
	<TasksForm {addTask} />
	<p class="mb-2">
		{#if tasks.length > 0}
			{totalDone} / {tasks.length} tasks completed
		{:else}
			Add a task to get started
		{/if}

		{#if tasks.length !== 0}
			<button class="cursor-pointer rounded-sm bg-blue-500 px-3 py-2 text-white shadow-sm outline outline-black/20"
				onclick={() => (tasks = [])}>Clear all tasks</button
			>
		{/if}
	</p>
	<section></section>
	<TaskList {tasks} {toggleDone} {removeTask} />
</main>

<style>
	main {
		margin: 1rem auto;
		max-width: 800px;
		padding: 0 20px;
	}

    p{
        display: flex;
        align-items: center;
        gap: 1rem;
        min-height: 50px;
    }
</style>
