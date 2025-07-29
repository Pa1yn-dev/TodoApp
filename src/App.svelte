<script>
  import TodoList from './components/TodoList.svelte'
  // Import from db or something.

  let todos = [];
  
</script>

<main>
  <TodoList {todos} />
</main>
