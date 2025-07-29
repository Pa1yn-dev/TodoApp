<script>
    let { addTodo, newTodoName = $bindable() } = $props();
</script>
<form> 
    <h2 class="label-wrapper">
        <label for="todo-0" class="label__lg"> What needs to be done? </label>
    </h2>
    <input type="text" bind:value={newTodoName} id="todo-0" autocomplete="off" class="input input__lg" />
    <button onclick={addTodo} type="button" class="btn btn__primary btn__lg"> Add </button>
</form>