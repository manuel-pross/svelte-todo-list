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
        padding: 0 15px;
    }

    .btn {
        cursor: pointer;
        box-sizing: unset;
        margin: 0;
        padding: 0.25rem 0.75rem;
        background-color: white;
        border-radius: 20px;
        min-width: 150px;
        border: 1px solid black;
    }

    .btn:hover {
        background-color: #dddd;
    }
</style>


<div class="delete-wrapper">
    <button class="btn" on:click={handleClickDeleteCompleted}>Delete completed</button>
    <button class="btn" on:click={handleClickDeleteAll}>Delete all</button>
</div>