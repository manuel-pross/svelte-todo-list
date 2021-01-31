<script>
    import { onMount } from "svelte";
    import { items } from "../stores";
    import TodoApi from "../TodoApi";
    import { v4 as uuidv4 } from "uuid";

    import Item from "../components/Item.svelte"
    import NewItem from "../components/NewItem.svelte"
    import DeleteItems from '../components/DeleteItems.svelte'

    let itemsSorted = [];

    $: {
        itemsSorted = [...$items];
        itemsSorted.sort((a, b) => {
            if (a.completed && b.completed) return 0;
            if (a.completed) return 1;
            if (b.completed) return -1;
        });
    }

	function handleNewItem(e) {
		$items = [
			{
				id: uuidv4(),
				text: e.detail,
				completed: false
			},
			...$items,
		];

		TodoApi.save($items);
	}

    function handleUpdate(e) {
        const index = $items.findIndex(item => item.id === e.detail.id);
        $items[index] = e.detail;
        TodoApi.save($items);
    }

    function handleDelete(e) {
        $items = $items.filter(item => item.id !== e.detail);
        TodoApi.save($items)
    }

    function handleClickDeleteCompleted() {
        $items = $items.filter(item => !item.completed);
        TodoApi.save($items);
    }

    function handleClickDeleteAll() {
        $items = [];
        TodoApi.save($items);
    }

    onMount(async () => {
        $items = await TodoApi.getAll();
    });

</script>

<style>
    .list {
        padding: 15px;
        text-align: center;
        color: white;
        font-weight: bold;
        font-size: 1.1em;
        margin: 0;
    }
</style>

<DeleteItems on:deleteAll={handleClickDeleteAll} on:deleteCompleted={handleClickDeleteCompleted} />
<ul class="list">
    <NewItem on:newItem={handleNewItem} />
    {#each itemsSorted as item (item)}
        <Item {...item} on:update={handleUpdate} on:delete={handleDelete} />
    {:else}
        <p class="list-status">No items exist</p>
    {/each}
</ul>