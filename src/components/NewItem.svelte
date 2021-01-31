<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    let value = "";

    function handleKeyUp({ key }) {
        if(key !== 'Enter' || value.length === 0) return;
        dispatch("newItem", value);
        value = "";
    }
</script>

<style>
    input {
        display: block;
        box-sizing: border-box;
        padding: 15px;
        border: none;
        outline: none;
        width: 100%;
        background: rgba(0, 0, 0, 0.25);
        color: white;
        font-weight: bold;
        font-size: 1em;
        cursor: pointer;
    }

    input::placeholder {
        color: white;
    }
</style>

<input type="text" on:keyup={handleKeyUp} bind:value placeholder="+ Add Item">