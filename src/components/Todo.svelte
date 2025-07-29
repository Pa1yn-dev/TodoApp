<script>
	let { todos } = $props();
	let total = $derived(todos.length);
	let completed = $derived(todos.filter((todo) => todo.completed).length);

	let newTodoName= "";
	let newTodoId = $derived(todos.length + 1);

	function addTodo() {
		todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }];
	}

    function deleteTodo(todo) {
        // Filters all rodo items that do not match the id of the deleted item into a new array that overwrites todos.
        todos = todos.filter((t) => t.id !== todo.id);
    }

	function checkAll() {
		// ... OP makes a copy of t and then we modify the completed property
		todos = todos.map(todo => (!todo.completed ? {...todo, completed: true} : todo));
	}

	function removeCompleted() {
		todos = todos.filter((t) => !t.completed == true);
	}
</script>

<!-- Todos.svelte -->
<div class="todoapp stack-large">
	<!-- NewTodo -->
	<form onsubmit={addTodo}>
		<h2 class="label-wrapper">
			<label for="todo-0" class="label__lg"> What needs to be done? </label>
		</h2>
		<input type="text" bind:value={newTodoName} id="todo-0" autocomplete="off" class="input input__lg" />
		<button onclick={addTodo} type="button" class="btn btn__primary btn__lg"> Add </button>
	</form>

	<!-- TodosStatus -->
	<h2 id="list-heading">{completed} out of {total} items completed</h2>

	<!-- Todos -->
	<ul role="list" class="todo-list stack-large" aria-labelledby="list-heading">
		{#each todos as todo (todo.id)}
			<li class="todo">
				<div class="stack-small">
					<div class="c-cb">
						<input onclick={() => todo.completed = !todo.completed} type="checkbox" id="todo-{todo.id}" checked={todo.completed} />
						<label for="todo-{todo.id}" class="todo-label"> {todo.name} </label>
					</div>
					<div class="btn-group">
						<button type="button" class="btn">
							Edit <span class="visually-hidden">{todo.name}</span>
						</button>
						<button onclick={() => deleteTodo(todo)} type="button" class="btn btn__danger">
							Delete <span class="visually-hidden">{todo.name}</span>
						</button>
					</div>
				</div>
			</li>
		{:else}
			<li>Nothing to do!</li>
		{/each}
	</ul>

	<hr />

	<!-- MoreActions -->
	<div class="btn-group">
		<button onclick={checkAll} type="button" class="btn btn__primary">Check all</button>
		<button onclick={removeCompleted} type="button" class="btn btn__primary">Remove completed</button>
	</div>
</div>
