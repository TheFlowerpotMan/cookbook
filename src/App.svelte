<script>
	import RecipeList from "./RecipeList.svelte";
</script>

<main>
	<h1>Welcome to Irina's Cookbook</h1>
	<RecipeList />
</main>

<style>
	main {
		padding: 1em;
		max-width: 85%;
		margin: 0 auto;
	}

	h1 {
		text-align: center;
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (max-width: 768px) {
		main {
			max-width: 85%;
			margin: auto;
		}
	}
</style>