<script>
	import Header from './components/Header.svelte';
	import List from './components/List.svelte';

</script>

<style>
	.container {
		width: 500px;
		padding: 15px;
		background: #009579;
	}

	:global(.container *) {
		font-family: sans-serif;
	}

	:global(body) {
		display: flex;
		justify-content: center;
	}

</style>

<div class="container">
	<Header />
	<List />
</div>