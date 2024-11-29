  <script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
    let number1 = $state(0);
    let number2 = $state(0);
    let amount = $state(0);
    let operations = $state([]);
    let operator = $state("");
    $effect(() => {
    console.log(number1);
    });
</script>
<Row>
  <Grid>
    <Card col={3}>
      <input type="number" bind:value={number1} />
    </Card>
    <Card col={3}>
      <input type="number" bind:value={number2} />
    </Card>
    <Card col={3}>
        {amount}
    </Card>
    <Card col={3}>
      <button onclick={() => {
        amount = number1 + number2;
        operations = [...operations, {number1, number2, amount, operator: '+' }];
      }}>Sum</button>
      <button onclick={() => {
        amount = number1 - number2;
        operations = [...operations, {number1, number2, amount, operator: '-' }];
      }}>Sub</button>
      <button onclick={() => {
        amount = number1 * number2;
        operations = [...operations, {number1, number2, amount, operator: '*' }];
      }}
      >
        Mul
      </button>
      <button
        onclick={() => {
          amount = number1 / number2;
          operations = [...operations, {number1, number2, amount, operator: '/' }];
        }}
        >
        Div
      </button>
    </Card>
    <Card col={3}>
      <ul>
        {#each operations as operation}
          <li onclick={() => {
            number1 = operation.number1;
            number2 = operation.number2;
            amount = operation.amount;
            operator = operation.operator;
          }}>
            {operation.number1} {operation.operator} {operation.number2} = {operation.amount}
          </li>
        {/each}
      </ul>
    </Card>
  </Grid>
</Row>
