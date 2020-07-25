<script>
  import { slide } from "svelte/transition";
  import Recipe from "./Recipe.svelte";

  let recipeList = null;
  let currentRecipeId = null;
  let searchCriteria = null;
  let tagMap = [];
  getAllRecipes();

  async function getAllRecipes() {
    let response = fetch(`https://benord.dev:8443/cookbook-api/recipes`)
      .then(response => response.json())
      .then(data => {
        recipeList = data;
        // TODO: Need to add tags into DB
        // buildTagMap();
      });
  }

  function buildTagMap() {
    for (let recipe of recipeList) {
      for (let tag of recipe.tags) {
        tagMap.push({ tag: tag, recipeId: recipe.id });
      }
    }
  }

  function showRecipe(id) {
    currentRecipeId = currentRecipeId && currentRecipeId === id ? null : id;
  }

  function search() {
    if (searchCriteria && searchCriteria.length > 0) {
      let filteredTags = tagMap.filter(x => x.tag.includes(searchCriteria));
      let filteredRecipes = [];
      for (let tag of filteredTags) {
        filteredRecipes.push(data.recipes.find(x => x.id === tag.recipeId));
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
  {#if recipeList}
    {#each recipeList as recipe}
      <h2 on:click={() => showRecipe(recipe.id)}>{recipe.id}</h2>
      {#if currentRecipeId && currentRecipeId === recipe.id}
        <div transition:slide>
          <Recipe class="recipe" {recipe} />
        </div>
      {/if}
    {/each}
  {/if}
</main>
