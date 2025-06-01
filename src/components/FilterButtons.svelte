<script>
  export let filter;
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  function setFilter(f) {
    dispatch('changeFilter', f);
  }
</script>

<div>
  <button on:click={() => setFilter('all')} disabled={filter === 'all'}>Усі</button>
  <button on:click={() => setFilter('active')} disabled={filter === 'active'}>Активні</button>
  <button on:click={() => setFilter('completed')} disabled={filter === 'completed'}>Завершені</button>
</div>