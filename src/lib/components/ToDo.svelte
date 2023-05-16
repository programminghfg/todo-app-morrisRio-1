<script>
        import { createEventDispatcher } from 'svelte';
        export let todoData = undefined;
        export let index = undefined;
        export const testProp = 'das ein test';

        const dispatch = createEventDispatcher();

        function triggerDelete() {
                dispatch('removeEvent', index);
        }
</script>

<div class="todo-entry" class:done={todoData.done}>
        <!-- text -->
        <p>index: {index}</p>
        <div>{todoData.text}</div>
        <!-- checkboxen -->
        <input type="checkbox" bind:checked={todoData.done} />
        <button
                class="delete"
                on:click={() => {
                        triggerDelete(index);
                }}
        >
                X
        </button>
</div>
<slot />

<style>
        .delete {
                background-color: white;
                border: none;
        }
        .delete:hover {
                background-color: grey;
                font-weight: 700;
        }
        .done {
                color: grey;
        }
        .todo-entry {
                display: flex;
        }
</style>
