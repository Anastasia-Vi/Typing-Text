<script>
    import { Card } from "../Grid"
    export let operations;
    export let clickedOperation;
</script>

<Card col={12}>
    <ul>
        {#each operations as operation}
          <li onclick={() => {
            clickedOperation = operation;
          }}>
            {operation.number1} {operation.operator} {operation.number2} = {operation.amount}
          </li>
        {/each}
    </ul>
    <slot />
</Card>