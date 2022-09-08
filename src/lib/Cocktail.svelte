<script lang="ts">
  import { scale } from "svelte/transition"
  export let drink: any
</script>

<div class="card border h-100" in:scale>
  <img
    src={drink.strDrinkThumb}
    class="card-img-top"
    alt={drink.strDrink}
    loading="lazy"
  />
  <div class="card-body text-white bg-dark">
    <h5 class="cart-title fw-bold text-warning">{drink.strDrink}</h5>

    <p class="card-text small">
      {drink.strInstructions}
    </p>
  </div>
  <div class="card-footer bg-dark text-warning text-muted">
    <p class="fst-italic small mb-0">
      {drink.strCategory}
    </p>
  </div>
</div>
