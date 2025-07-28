<script>
  import Todos from './components/Todo.svelte'
  // Import from db or something.
  let todos = []
  
</script>

<main>
  <Todos todos={todos}/>
</main>
