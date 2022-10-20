<script>
  import Todo from "./Todo.svelte";

  let todoList = [];
  let newItem = "";
  const handleAddTodo = () => {
    todoList = [...todoList, { text: newItem, completed: false }];
    newItem = "";
  };
  const handleAddToCompleted = (index) => {
    todoList[index].completed = true;
    todoList = todoList;
  };
  const handleRedoTodo = (index) => {
    todoList[index].completed = false;
    todoList = todoList;
  };
  const handleRemoveTodo = (index) => {
    todoList.splice(index, 1);
    todoList = todoList;
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
            on:remove={() => handleRemoveTodo(index)}
            on:complete={() => handleAddToCompleted(index)}
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
            on:remove={() => handleRemoveTodo(index)}
            on:redo={() => handleRedoTodo(index)}
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
