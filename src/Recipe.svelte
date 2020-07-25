<script>
  export let recipe;
  let ingredients = recipe.ingredients;
  let instructions = recipe.instructions;
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
</style>

<main>
  <span class="section-title">Prep:</span>
  {recipe.prep_time}&nbsp;&nbsp;&nbsp;&nbsp;
  <span class="section-title">Cook:</span>
  {recipe.cook_time}&nbsp;&nbsp;&nbsp;&nbsp;
  <span class="section-title">Serves:</span>
  {recipe.servings}
  {#if recipe.description}
    <div class="section-title">Description</div>
    <p>{recipe.description}</p>
    <hr />
  {/if}
  <div class="section-title">Ingredients</div>
  {#each ingredients as ingredient}
    <div class="list-item">{ingredient.amount}{ingredient.unit} {ingredient.title}</div>
  {/each}
  <div class="section-title">Directions</div>
  {#each instructions as instruction, i}
    <div class="list-item">{i + 1} - {instruction.step}</div>
  {/each}
</main>
