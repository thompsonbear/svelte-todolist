<script>
    import { fly } from 'svelte/transition';

    let formText = '';

    let todos = [
        { text: 'Learn Svelte'},
        { text: 'Write a simple todo app'},
        { text: 'Profit?'}
    ];

    function addTodo() {
        if (formText){
            todos = [...todos, {text: formText}];
            formText='';
        }
    }

    function rmTodo(index) {
        todos.splice(index, 1)
        todos = todos;
    }
</script>

<main>
    <div class="todo-list">
        <div class="todo-form">
            <input class="todo-input" placeholder="Add a new Todo here..." bind:value={formText}>
            <button class="btn btn-add" on:click={addTodo} onclick="this.blur();">
                <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" class="bi bi-plus-circle-fill" viewBox="0 0 16 16">
                <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM8.5 4.5a.5.5 0 0 0-1 0v3h-3a.5.5 0 0 0 0 1h3v3a.5.5 0 0 0 1 0v-3h3a.5.5 0 0 0 0-1h-3v-3z"/>
                </svg>
            </button>
        </div>
        
        {#each todos as todo, index(todo)}
        <div class="todo-item" out:fly={{x:10}} in:fly={{y:50}}>
            <input class="todo-input" value={todo.text}>
            <button class="btn" on:click={rmTodo(index)}>
                <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" class="bi bi-trash-fill" viewBox="0 0 16 16">
                <path d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z"/>
                </svg>
            </button>
        </div>
        {/each}
    </div>
</main>

<style>
.btn {
    cursor: pointer;
    border: none;
    background: #6E757B;
    width: 4rem;
    height: 4rem;
    opacity: 0.8;
    transition: all 0.1s ease-in-out;
    outline: none;
}

.btn-add{
    background: #FB6C05;
}

.btn svg{
    fill: white;
    width: 1.25rem;
    transition: all 0.1s ease-in-out;
}

.btn:hover, .btn:focus{
    opacity: 1;
}
 
.btn:hover svg, .btn:focus svg{
    transform: scale(1.1);
}

.todo-input{
    border: none;
    font-size: 1rem;
    background: white;
    padding-left: 1rem;
    padding-right: 1rem;
    height: 4rem;
    width: 24rem;
    margin-right: .25rem;
    outline: none;
    transition: all 0.1s ease-in-out;
}

.todo-input:hover, .todo-input:focus{
    background: #FFEEE2;
}

.todo-form{
    display: flex;
}

.todo-item{
    margin-top: .25rem;
    box-shadow: 1px 26px 41px -28px rgba(0,0,0,0.75);
    display: flex;
}

.todo-list{
    margin-top: 150px;
}

</style>
