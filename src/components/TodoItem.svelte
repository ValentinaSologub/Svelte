<script>
  export let todo;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
</script>

<li>
  <input
    type="checkbox"
    bind:checked={todo.done}
    on:change={() => dispatch('toggleDone', todo.id)}
  />
  <span style="text-decoration: {todo.done ? 'line-through' : 'none'}">
    {todo.text}
  </span>
  <button on:click={() => dispatch('removeTodo', todo.id)}>❌</button>
</li>