<script lang="ts">
    import { fade } from 'svelte/transition';
	import type { Task } from "$lib/types";
    let { tasks, toggleDone, removeTask }: {
        tasks: Task[],
        toggleDone: (task: Task) => void
        removeTask: (index: string) => void
    } = $props();
</script>

<section>
    {#each tasks as task (task.id)}
        <article transition:fade class="outline outline-black/20 p-2 rounded-sm flex justify-between items-center">
            <label>
                <input type="checkbox" checked={task.done} onchange={() => toggleDone(task)} />
                <span class:done={task.done}>{task.title}</span>
            </label>
            <button class="cursor-pointer rounded-sm px-3 py-2 bg-blue-500 text-white shadow-sm outline outline-black/20" onclick={() => removeTask(task.id)}>Remove</button>
        </article>
    {/each}
</section>

<style>
    article {
        display: flex;
        align-items: center;
        margin-bottom: 0.5rem;
    }

    .done {
        text-decoration: line-through;
    }
</style>