<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  let form = $state({});
  let accordion = $state([]);
</script>

<Row>
 <Grid>
  <Card col={6}>
    <h1>Form</h1>
    <input type="text" bind:value={form.title} />
    <input type="text" bind:value={form.description} />
  </Card>
  <Card col={6}>
   <button onclick={() => {
    accordion = [...accordion, {title: form.title, description: form.description, show: false}];
   }}>
    Add form
   </button>
  </Card>
  <Card col={12}>
    <ul>
      {#each accordion as item}
        <li class:active={item.show} onclick={() => {
            item.show = !item.show;
        }}>
        <div class="accordion-title">{item.title}</div>
        <div class="accordion-description">{item.description}</div>
        </li>
      {/each}
    </ul>
  </Card>
 </Grid>
</Row>


<style>
    li {
    list-style: none;
    border: 1px solid #ccc;
    }
    .accordion-title {
        font-weight: bold;
        padding: 10px;
    }
    .accordion-description {
        display: none;
    }
    .active .accordion-description {
        display: block;
    }
</style>
