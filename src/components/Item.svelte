<script>
    import { createEventDispatcher } from "svelte";

    export let id, text, completed;

    const dispatch = createEventDispatcher();

    function triggerUpdate() {
        dispatch("update", {id, text, completed});
    }

    function handleDoubleClick() {
        const yes = confirm("Are you sure you wish to delete this item");

        if(yes)
            dispatch("delete", id);
    }
</script>

<style>
    .item {
        display: flex;
        justify-content: start;
        align-items: center;
        padding: 10px;
        background: white;
        margin-bottom: 1rem;
    }

    .item.completed {
        background: #dddd;
    }

    .item.completed .text-input {
        color: #555;
        text-decoration: line-through;
    }

    .item:focus-within { /*Wenn ein inneres Element den Focus bekommt bekommt dieses Element ihn ebenfalls */
        background: rgba(255, 255, 255, 0.8);
    }

    .text-input {
        flex-grow: 1;
        background: none;
        border: none;
        outline: none;
        font-weight: 500;
        font-size: 1em;
        margin: 0 1rem 0 0;
    }

    .completed-checkbox {
        margin-bottom: 0;
    }
</style>

<li class="item" class:completed on:dblclick={() => handleDoubleClick()}>
    <input 
        class="text-input" 
        type="text" 
        bind:value={text} 
        readonly={completed}
        on:keyup={({key, target}) => key === 'Enter' && target.blur()}
        on:blur={() => triggerUpdate()} />
    <input 
        class="completed-checkbox" 
        type="checkbox" 
        bind:checked={completed}
        on:change={() => triggerUpdate()} />
</li>