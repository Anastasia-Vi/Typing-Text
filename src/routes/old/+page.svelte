<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  let products = $state([]);
  let carts = $state([]);
  $effect(() => {
    console.log(products);
  });
</script>
<Row>
  <Grid>
    <Card>
      <ul>
        {#each products as product}
          <li>
            <input type="text" bind:value={product.name} />
            <input type="number" bind:value={product.price} />
            <button
              onclick={() => {
                carts = [...carts, product];
              }}
            >
              Add to cart
            </button>
          </li>
        {/each}
      </ul>
      <button
        onclick={() => {
          products = [...products];
        }}
      >
        Save
      </button>
    </Card>
    <Card col={12}>
      <button
        onclick={() => {
          products = [
            ...products,
            { name: "Product " + products.length, price: 0, id: products.length },
          ];
        }}
      >
        Add new product
      </button>
    </Card>
    <Card>
      <ul>
        {#each carts as cart}
          <li>
            {cart.name}, {cart.price}
          </li>
        {/each}
      </ul>
    </Card>
  </Grid>
</Row>