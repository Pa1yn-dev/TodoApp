<script>
	import NewItem from "./newItem.svelte";
	import Status from "./Status.svelte";
	import Item from "./Item.svelte";
	import MoreActions from "./MoreActions.svelte";

	let { todos } = $props();

	let newTodoName = $state();
	let newTodoId = $derived(todos.length + 1);

	function addTodo() {
		todos = [...todos, { id: newTodoId, name: newTodoName, completed: false }];
	}

	function checkItem(todo) {
		todo.completed = !todo.completed
		// Reassigns array to itself to force a reactivity update, as svelte's reactivity system does not track mutation of properties.
		todos = [...todos];
	}

	function editItem(todo) {
        // Filters all rodo items that do not match the id of the item to be edited.
        todos = todos.filter((t) => t.id !== todo.id);
		newTodoName = todo.name;
    }

    function removeItem(todo) {
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

<div class="todoapp stack-large">
	
	<NewItem {addTodo} bind:newTodoName/>
	<Status bind:todos />
	<ul role="list" class="todo-list stack-large" aria-labelledby="list-heading">
		{#each todos as todo (todo.id)}
			<li class="todo">
				<Item {todo} checkItem = {() => checkItem(todo)} removeItem = {() => removeItem(todo)} editItem={() => editItem(todo)}/>
			</li>
		{:else}
			<li>Nothing to do!</li>
		{/each}
	</ul>
	<hr />
	<MoreActions {checkAll} {removeCompleted} />
</div>
