<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  import { BtnComp } from "$lib/ui/BtnComp";
  import { FourBnt } from "$lib/ui/FourBnt";
  import { Amount } from "$lib/ui/Amount";
  let click1 = $state(0);
  let click2 = $state(0);
  let operator = $state('+');
</script>

<div class="container">
  <Row>
    <Grid>
      <Card col={3}>
        <BtnComp bind:count={click1}/>
      </Card>
      <Card col={3}>
        <BtnComp bind:count={click2}/>
      </Card>
      <Card col={3}>
        <Amount a={click1} b={click2} operator={operator}/>
      </Card>
      <Card col={3}>
        <FourBnt bind:operator={operator} />
      </Card>
    </Grid>
  </Row>
</div>

<style>
  .container {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #e0eafc 0%, #cfdef3 100%);
    padding: 2rem;
  }
</style>