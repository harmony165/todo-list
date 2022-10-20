<script>
  import { createEventDispatcher } from "svelte";

  export let todo;
  const dispatch = createEventDispatcher();
  const handleComplete = () => {
    dispatch("complete");
  };
  const handleRemove = () => {
    dispatch("remove");
  };
  const handleRedo = () => {
    dispatch("redo");
  };
</script>

<div class={todo.completed ? "todo-row completed" : "todo-row"}>
  {#if todo.completed === true}
    <button on:click={handleRedo}>
      <i class="mi-undo" />
    </button>
  {:else}
    <button on:click={handleComplete}>
      <i class="mi mi-circle-check" />
    </button>
  {/if}
  <div class="todo-text">{todo.text}</div>
  <button on:click={handleRemove}> <i class="mi mi-circle-error" /></button>
</div>

<style>
  .todo-row {
    margin: 10px;
    padding: 10px;
    width: 100%;
    color: black;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-radius: 20px;
    background-color: #edaf02;
  }
  .todo-row:hover {
    box-shadow: 1px 1px 0px black, 2px 2px 0px black, 3px 3px 0px black,
      4px 4px 0px black, 5px 5px 0px black, 6px 6px 0px black;
  }

  .completed {
    background-color: greenyellow;
  }
  .completed button:hover {
    border-color: greenyellow;
  }
</style>
