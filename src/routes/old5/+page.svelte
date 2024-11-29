<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  import { Color } from "$lib/ui/Color";
  import { Color2 } from "$lib/ui/Color2";
  let name = $state('');
  let backgroundColor = $state('white')

  
</script>
  <Row>
    <Grid>
      <Card col={12}>
        <input type="text" style="background-color:{backgroundColor}" bind:value={name} />
      </Card>
        <Card col={6}>
        <Color bind:backgroundColor={backgroundColor}/> 
        <Color2 bind:backgroundColor2={backgroundColor}/>
        </Card>
    </Grid>
  </Row>

<style>
  input{
        padding: 1rem;
        box-sizing: border-box;
        text-align: right;
        font-size: 20px;
        }
</style>
