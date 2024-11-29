<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  import { ListOperation } from "$lib/ui/ListOperation";
  let number1 = $state(0);
  let operator = $state('');
  let numberSaved = $state(0);
  let o = $state([]);
  let clickedOperation = $state(null);
  $effect(() => {
    console.log(clickedOperation);
  });
  </script>

 <div class="container">
    <Row>
        <Grid>
            <Card noPadding col={12}>
            <input type = "number" bind:value={number1} />
            </Card>
                <Card center background="#eee" col={2} onclick={() => {
                    numberSaved = number1;
                    number1 = 0;
                    operator = '+';
                    }}>
                    +
                </Card>
                <Card center background="#eee" col={2} onclick={() => {
                    numberSaved = number1;
                    number1 = 0;
                    operator = '-';
                    }}>
                    -
                </Card>
                <Card center background="#eee" col={2} onclick={() => {
                    numberSaved = number1;
                    number1 = 0;
                    operator = '*';
                    }}>
                    *
                </Card>
                <Card center background="#eee" col={2} onclick={() => {
                    numberSaved = number1;
                    number1 = 0;
                    operator = '/';
                    }}>
                    /
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = 0;
                    }}>
                    Delete
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 7;
                    }}>
                    7
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 8;
                    }}>
                    8
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 9;
                    }}>
                    9
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 4;
                    }}>
                    4
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 5;
                    }}>
                    5
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 6;
                    }}>
                    6
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 1;
                    }}>
                    1
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 2;
                    }}>
                    2
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 3;
                    }}>
                    3
                </Card>
                <Card center background="#eee" col={4} onclick={() => {
                        number1 = number1 * 10 + 0;
                    }}>
                    0
                </Card>
                <Card center background="#eee" col={8} onclick={() => {
                    let amount = 0;
                    if(operator == '+'){
                        amount = numberSaved + number1;
                    } else if(operator == '-'){
                        amount = numberSaved - number1;
                    } else if(operator == '*'){
                        amount = numberSaved * number1;
                    } else if(operator == '/'){
                        amount = numberSaved / number1;
                    }
                    o.push({
                        number1: numberSaved,
                        operator: operator,
                        number2: number1,
                        amount: amount
                    });
                    number1 = amount;
                    }}>
                    =
                </Card>
                    <ListOperation 
                        operations={o} 
                        bind:clickedOperation={clickedOperation} 
                    />
        </Grid>
    </Row>
  </div>
  
<style>
    .container{
        width: 300px;
    }
    input{
        width: 100%;
        padding: 1rem;
        box-sizing: border-box;
        text-align: right;
    }
</style>