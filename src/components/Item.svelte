<script>
    let {todo = $bindable(), checkItem, removeItem, editItem} = $props();
</script>
<div class="stack-small">
    <div class="c-cb">
        <input
            onclick={checkItem}
            type="checkbox"
            id="todo-{todo.id}"
            checked={todo.completed}
        />
        <label for="todo-{todo.id}" class="todo-label"> {todo.name} </label>
    </div>
    <div class="btn-group">
        <button onclick={editItem} type="button" class="btn">
            Edit <span class="visually-hidden">{todo.name}</span>
        </button>
        <button onclick={removeItem} type="button"class="btn btn__danger">
            Delete <span class="visually-hidden">{todo.name}</span>
        </button>
    </div>
</div>
