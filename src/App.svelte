<script>
  import TodoItem from './components/TodoItem.svelte';
  import FilterButtons from './components/FilterButtons.svelte';

  let todos = [];
  let newTodo = '';
  let filter = 'all';

  function addTodo() {
    if (newTodo.trim()) {
      todos = [...todos, { id: Date.now(), text: newTodo, done: false }];
      newTodo = '';
    }
  }

  function toggleDone(id) {
    todos = todos.map(todo => todo.id === id ? { ...todo, done: !todo.done } : todo);
  }

  function removeTodo(id) {
    todos = todos.filter(todo => todo.id !== id);
  }

  $: filteredTodos = filter === 'all'
    ? todos
    : filter === 'active'
    ? todos.filter(todo => !todo.done)
    : todos.filter(todo => todo.done);
</script>

<h1>To-Do App</h1>
<input bind:value={newTodo} on:keydown={(e) => e.key === 'Enter' && addTodo()} placeholder="Нове завдання..." />
<button on:click={addTodo}>Додати</button>

<FilterButtons {filter} on:changeFilter={(e) => filter = e.detail} />

<ul>
  {#each filteredTodos as todo (todo.id)}
    <TodoItem {todo} on:toggleDone on:removeTodo />
  {/each}
</ul>
