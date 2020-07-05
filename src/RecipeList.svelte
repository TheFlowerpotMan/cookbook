<script>
  import { slide } from "svelte/transition";
  import data from "./kitchen-recipes.js";
  import Recipe from "./Recipe.svelte";

  let recipeList = data.recipes;
  let currentRecipe = null;
  let searchCriteria = null;
  let tagMap = [];
  let importedData = getResult();

  for (let recipe of data.recipes) {
    for (let tag of recipe.tags) {
      tagMap.push({ tag: tag, recipeTitle: recipe.title });
    }
  }

  async function getResult() {
    let response = fetch(`https:benord.dev:8443/cookbook-api/recipes`).then(
      data => {
        debugger;
        return data;
      }
    );
  }

  function showRecipe(title) {
    currentRecipe = currentRecipe && currentRecipe === title ? null : title;
  }

  function search() {
    if (searchCriteria && searchCriteria.length > 0) {
      let filteredTags = tagMap.filter(x => x.tag.includes(searchCriteria));
      let filteredRecipes = [];
      for (let tag of filteredTags) {
        filteredRecipes.push(
          data.recipes.find(x => x.title === tag.recipeTitle)
        );
      }
      const unique = new Set(filteredRecipes);
      recipeList = [...unique];
    } else {
      recipeList = data.recipes;
    }
  }
</script>

<style>
  main {
    max-width: 70%;
    margin: 0 auto;
  }
  h2 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 2em;
    font-weight: 100;
  }
  h2:hover {
    cursor: pointer;
    font-weight: 200;
  }
</style>

<main>
  <input
    bind:value={searchCriteria}
    on:change={search}
    placeholder="Search here..." />
  <div>{importedData}</div>
  {#each recipeList as recipe}
    <h2 on:click={() => showRecipe(recipe.title)}>{recipe.title}</h2>
    {#if currentRecipe && currentRecipe === recipe.title}
      <div transition:slide>
        <Recipe class="recipe" title={recipe.title} />
      </div>
    {/if}
  {/each}
</main>
