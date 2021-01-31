<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();


    function handleClickDeleteAll() {
        dispatch("deleteAll");
    }

    function handleClickDeleteCompleted() {
        dispatch("deleteCompleted");
    }

</script>

<style> 
    .delete-wrapper {
        display: flex;
        justify-content: space-between;
    }
</style>


<div class="delete-wrapper">
    <button on:click={handleClickDeleteCompleted}>Delete completed</button>
    <button on:click={handleClickDeleteAll}>Delete all</button>
</div>