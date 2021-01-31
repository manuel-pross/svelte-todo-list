<script>
    import { items } from '../stores';

    $: itemCount = $items.length; //Wann immer sich items ändert, wird itemCount neu zugewiesen
    $: completedItemCount = $items.filter(item => item.completed).length; 
</script>

<style>
    .header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 15px 20px;
        color: white;
        font-weight: bold;
        font-size: 1.5em;
        background: rgba(0, 0, 0, 0.1);
        margin-bottom: 1rem;
    }
</style>

<div class="header">
    <span>Manuel's To-Do List</span>
    <span>{completedItemCount}/{itemCount}</span>
</div>