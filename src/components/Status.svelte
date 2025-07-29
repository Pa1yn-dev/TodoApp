<script>
    let { todos = $bindable()} = $props();

    let total = $derived(todos.length);
	let completed = $derived(todos.filter((todo) => todo.completed).length);
</script>
<h2 id="list-heading">{completed} out of {total} items completed</h2>
