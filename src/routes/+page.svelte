<script>
        import { onMount } from 'svelte';
        import { browser } from '$app/environment';
        import ToDo from '../lib/components/ToDo.svelte';
        let todoText = '';
        let todos = [];

        let test;

        onMount(() => {
                if (browser) {
                        const storedTodos = JSON.parse(localStorage.getItem('todos'));
                        if (storedTodos) {
                                todos = storedTodos;
                        }
                }
        });

        function saveTodos() {
                // Save todos to local storage
                if (browser) {
                        localStorage.setItem('todos', JSON.stringify(todos));
                }
        }

        function addTodo() {
                todos.push({ text: todoText, done: false });
                todos = todos;
                todoText = '';
                // Save todos to local storage
                saveTodos();
        }

        function remove(event) {
                //delete entry
                let index = event.detail;
                console.log(index);
                todos.splice(index, 1);
                todos = todos;
                saveTodos();
        }
</script>

<h1>TODO APP</h1>

<!-- textfeld -->
<input type="text" class="todo-input" bind:value={todoText} />
<!-- button add -->
<button on:click={addTodo}>ADD</button>

{#each todos as todo, i}
        <!-- todo -->
        <ToDo todoData={todo} bind:testProp={test} index={i} on:removeEvent={remove} />
{/each}
