<script>
        import { onMount } from "svelte";
        import { browser } from "$app/environment";

        let todoText = "";
        let todos = [];

        onMount(() => {
                if (browser) {
                        const storedTodos = JSON.parse(
                                localStorage.getItem("todos")
                        );
                        if (storedTodos) {
                                todos = storedTodos;
                        }
                }
        });

        function saveTodos() {
                // Save todos to local storage
                if (browser) {
                        localStorage.setItem("todos", JSON.stringify(todos));
                }
        }

        function addTodo() {
                todos.push({ text: todoText, done: false });
                todos = todos;
                todoText = "";
                // Save todos to local storage
                saveTodos();
        }

        function remove(index) {
                //delete entry
                todos.splice(index, 1);
                todos = todos;
                saveTodos();
        }
</script>
<div class="all">
<div class="actionbuttons">
        <button class="abutton" on:click={remove}>Papierkorb</button>
        <button class="abutton" on:click={saveTodos}>Archiv</button>
</div>
<div>
        <img class="catheaderimg" src="/src/Katzen.png" alt="Katze" />
</div>
<div class="sidebuttons">
        <button class="sbutton1" on:click={addTodo} /><br />
        <button class="sbutton2" on:click={addTodo} /><br />
        <button class="sbutton3" on:click={addTodo} /><br />
        <button class="sbutton4" on:click={addTodo} />
</div>

<!--
<h1>TODO APP</h1>
-->
<!-- textfeld -->
<div class="center-block">
        <input type="text" class="todo-input" bind:value={todoText} />
        <!-- button add -->
        <button class="addbutton" on:click={addTodo}>ADD</button>
</div>
<h1 style="font-family: 'Nanum Pen Script', cursive;font-size: 62px;">Do Whatchu Gotta Do</h1>
</div>
{#each todos as todo, index}
        <!-- todo -->
        <div class="todo-entry" class:done={todo.done}>
                <!-- text -->
                <div style="font-family: 'Nanum Pen Script', cursive;"><h2>{todo.text}</h2></div>
                <!-- checkboxen -->
                <input type="checkbox" bind:value={todo.done} />
                <button
                        class="delete"
                        on:click={() => {
                                remove(index);
                        }}>X</button
                >
        </div>
{/each}
