<script>
  import Todo from "./Todo.svelte";

  const todosJson = localStorage.getItem("todos");
  let todoList = todosJson ? JSON.parse(todosJson) : [];
  let newItem = "";
  $: localStorage.setItem("todos", JSON.stringify(todoList));

  const handleAddTodo = () => {
    todoList = [...todoList, { text: newItem, completed: false }];
    newItem = "";
  };
  const handleAddToCompleted = (item) => {
    item.completed = true;
    todoList = todoList;
  };
  const handleRedoTodo = (item) => {
    item.completed = false;
    todoList = todoList;
  };
  const handleRemoveTodo = (item) => {
    todoList = todoList.filter((todo) => todo !== item);
  };
</script>

<div>
  <form class="form" on:submit|preventDefault={handleAddTodo}>
    <input
      class="input-bar"
      type="text"
      bind:value={newItem}
      placeholder="Add a Todo"
    />
    <button type="submit"><i class="mi mi-circle-add" /></button>
  </form>
  <div class="todo-container">
    <div class="todo-column">
      <h2>Pending</h2>
      {#each todoList as item, index}
        {#if item.completed === false}
          <Todo
            todo={item}
            on:remove={() => handleRemoveTodo(item)}
            on:complete={() => handleAddToCompleted(item)}
          />
        {/if}
      {/each}
    </div>
    <div class="todo-column">
      <h2>Completed</h2>
      {#each todoList as item, index}
        {#if item.completed === true}
          <Todo
            todo={item}
            on:remove={() => handleRemoveTodo(item)}
            on:redo={() => handleRedoTodo(item)}
          />
        {/if}
      {/each}
    </div>
  </div>
</div>

<style>
  .todo-column {
    width: 450px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 10px;
  }
  .todo-container {
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: space-between;
  }
  .form {
    display: flex;
  }
  .input-bar {
    margin: 1;
    flex-grow: 1;
  }
</style>
