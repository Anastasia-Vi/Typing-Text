<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  import { onDestroy } from "svelte";
  import { browser } from "$app/environment";
  let text = $state("Chinese Dragon");
  let letters = $state([]);
  let started = $state(false);
  let timer = $state(0);
  let intervalId;
  let scores = $state(browser ? JSON.parse(localStorage.getItem('typingScores')) || [] : []);
  $effect(() => {
    console.log(letters);
  })
  function on_key_up(event) {
    let key = event.key.toLowerCase();
    console.log(event.key);
    if (started === false) {
      if(key === ' ') {
        start();
      }
      return;
    }
    if (key === letters[0]) {
    //This is code check if the key pressed is the first letter of the array and if it is, it removes it from the array
      letters = letters.slice(1);
      if (letters.length === 0) {
      const now = new Date();
      clearInterval(intervalId)
      started = false;
      scores = [...scores, {time: timer, now: now.getTime()}];
      scores.sort((a, b) => a.time - b.time);
      localStorage.setItem('typingScores', JSON.stringify(scores));//Save the scores to local storage. setItem tells save variable typingScores the stringified scores
      }
    }
  }
  function start() {
    letters = text.toLowerCase().split('');
    started = true;
    timer = 0;
    intervalId = setInterval(() => {
      timer++;
    }, 1000);
  }
  // Clean up interval when component is destroyed
  onDestroy(() => {
    if (intervalId) clearInterval(intervalId);
  });
</script>

<svelte:window
    on:keyup={on_key_up}
/>
<Row>
    <Grid>
      <Card col={12}>
        <h1>Typing Test</h1>
        <div>{letters.join('')}</div>
        {#if started === false}
       <button on:click={start}>Start</button>
       {/if}
       <div>Time: {timer} seconds</div>
       <div>
        <ul>
          {#each scores as score}
            <li> Score: {score.time} seconds at the time of {new Date(score.now).toLocaleString()} </li>
          {/each}
        </ul>
      </Card>
    </Grid>
  </Row>
