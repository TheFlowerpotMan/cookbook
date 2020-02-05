<script>
  import data from "./kitchen-recipes.js";

  export let title;
  let recipe = data.recipes.find(x => x.title === title);
</script>

<style>
  main {
    font-weight: 100;
    margin-left: 40px;
  }

  .section-title {
    text-align: center;
    font-weight: 300;
  }

  .list-item {
    padding-top: 15px;
  }
  @media (max-width: 768px) {
		main {
			max-width: 85%;
			margin: auto;
      margin-left: 10px;
		}
  }
</style>

<main>
  <span class="section-title">Prep:</span>
  {recipe.time.prep}&nbsp;&nbsp;&nbsp;&nbsp;
  <span class="section-title">Cook:</span>
  {recipe.time.cook}&nbsp;&nbsp;&nbsp;&nbsp;
  <span class="section-title">Serves:</span>
  {recipe.servings}
  {#if recipe.description}
    <div class="section-title">Description</div>
    <p>{recipe.description}</p>
    <hr />
  {/if}
  <div class="section-title">Ingredients</div>
  {#each recipe.ingredients as ingredient}
    <div class="list-item">{ingredient.amount} {ingredient.title}</div>
  {/each}
  <div class="section-title">Directions</div>
  {#each recipe.instructions as instruction, i}
    <div class="list-item">{i + 1} - {instruction.step}</div>
  {/each}
</main>
