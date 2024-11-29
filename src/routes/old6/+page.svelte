<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  import { Accordion } from "$lib/ui/Accordion";
  let accordions = $state([]);
</script>

  <Row>
    <Grid>
      <Card col={12}>
      <button onclick={() => {
        accordions = [...accordions, {title: "Accordion " + accordions.length}];
      }}>
        Add accordion
      </button>
      </Card>
      <Card col={12}>
      <ul>
        {#each accordions as accordion}
          <li>
            <Accordion {accordion} />
            <button onclick={() => {
              accordions = accordions.filter(i => i !== accordion);
            }}>Delete</button>
          </li>
        {/each}
      </ul>
      </Card>
    </Grid>
  </Row>

  