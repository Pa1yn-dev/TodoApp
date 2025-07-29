<script>
    let { checkAll, removeCompleted } = $props();
</script>

<div class="btn-group">
    <button onclick={checkAll} type="button" class="btn btn__primary"
        >Check all</button
    >
    <button onclick={removeCompleted} type="button" class="btn btn__primary"
        >Remove completed</button
    >
</div>
