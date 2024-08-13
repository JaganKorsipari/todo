<script>
    let newTodo = "";
    let todos = [];

    function addTodo() {
        if (newTodo.trim()) {
            todos = [...todos, { text: newTodo, completed: false }];
            newTodo = "";
            sortTodos();
        }
    }

    function toggleComplete(index) {
        todos[index].completed = !todos[index].completed;
        sortTodos();
    }

    function deleteTodo(index) {
        todos = todos.filter((_, i) => i !== index);
    }

    function sortTodos() {
        todos = todos.slice().sort((a, b) => a.completed - b.completed);
    }
</script>

<style>
    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        background-color: #f0f4f8;
        color: #333;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }

    main {
        background: rgb(249, 204, 212);
        padding: 20px;
        border-radius: 10px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 480px;
		margin-left: 500px;
		margin-top: 200px;
    }

    h1 {
        margin: 0;
        font-size: 24px;
        text-align: center;
        color: #0077b6;
    }

    input[type="text"] {
        width: 476px;
        padding: 10px;
        border: 1px solid #0077b6;
        border-radius: 5px;
        outline: none;
		margin-top: 20px;
    }

    button {
        padding: 10px 15px;
        background-color: #0077b6;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        margin-left: 420px;
        transition: background-color 0.3s;
		
    }

    button:hover {
        background-color: #005f87;
    }

    ul {
        list-style-type: none;
        padding: 0;
        margin-top: 20px;
    }

    li {
        display: flex;
        align-items: center;
        padding: 10px;
        margin-bottom: 10px;
        background-color: #f9f9f9;
        border: 1px solid #ddd;
        border-radius: 5px;
        transition: background-color 0.3s;
    }

    li:hover {
        background-color: #e9e9e9;
    }

    input[type="checkbox"] {
        margin-right: 10px;
    }

    .completed {
        text-decoration: line-through;
        color: #888;
    }

    .delete-btn {
        background-color: transparent;
        color: #e74c3c;
        border: none;
        cursor: pointer;
        margin-left: auto;
        font-size: 16px;
        transition: color 0.3s;
    }

    .delete-btn:hover {
        color: #c0392b;
    }
</style>

<main>
    <h1>Todo List</h1>

    <div>
        <input
            type="text"
            bind:value={newTodo}
            placeholder="Add a new task"
            on:keydown="{(e) => e.key === 'Enter' && addTodo()}"
        />
        <button on:click={addTodo}>Add</button>
    </div>

    <ul>
        {#each todos as todo, index}
            <li>
                <input
                    type="checkbox"
                    checked={todo.completed}
                    on:change={() => toggleComplete(index)}
                />
                <span class:completed={todo.completed}>{todo.text}</span>
                <button class="delete-btn" on:click={() => deleteTodo(index)}>
                    &#x1F5D9;
                </button>
            </li>
        {/each}
    </ul>
</main>
