<script lang="ts">
  import axios from "axios"
  import Cocktail from "./Cocktail.svelte"
  import NoCocktail from "./NoCocktail.svelte"

  let drinks: Array<any> = []
  let drinkName: string = "Margarita"

  const getDrinks = async () => {
    const url: string = `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${drinkName}`
    const { data } = await axios.get(url)

    drinks = data.drinks || []
    drinkName = ""
  }

  const handleSubmit = () => {
    promise = getDrinks()
  }

  let promise = getDrinks()
</script>

<div class="container my-3 text-center">
  <form class="d-flex gap-3 mb-3" on:submit|preventDefault={handleSubmit}>
    <h2 class="text-nowrap text-warning">Search Cocktail</h2>
    <input
      type="text"
      class="form-control bg-dark text-white"
      placeholder="Drink name"
      bind:value={drinkName}
    />
    <button type="submit" class="btn btn-outline-warning fw-bold">Search</button
    >
  </form>

  {#await promise}
    <div class="spinner-grow text-light" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  {:then drinksResponse}
    <div class="row g-3">
      {#each drinks as drink}
        <div class="col-12 col-sm-6 col-md-4 col-lg-3">
          <Cocktail {drink} />
        </div>
      {:else}
        <NoCocktail />
      {/each}
    </div>
  {/await}
</div>
