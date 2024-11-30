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
  function on_key_down(event){
    event.preventDefault();
  }
  function start() {
    letters = text.toLowerCase().split('');
    started = true;
    timer = 0;
    intervalId = setInterval(() => {//setInterval is a function that calls a function repeatedly at specified intervals
      timer = timer + 10;
    }, 10);
  }
  function restart(){
    started = false;
    timer = 0;
    letters = [];
    clearInterval(intervalId);
  }
  // Clean up interval when component is destroyed
  onDestroy(() => {
    if (intervalId) clearInterval(intervalId);
  });
</script>

<svelte:window
    on:keyup={on_key_up} on:keydown={on_key_down}
/>
  <Row>
    <Grid>
        <Card col={12}>
          <h1 class="title">Typing Test</h1>
          <div class="letters">{letters.join('')}</div>
          <input type="text"/>
          <div class="controls">
            {#if started === false}
              <button class="btn" on:click={start}>Start</button>
            {/if}
            <button class="btn" on:click={restart}>Restart</button>
          </div>
          <div class="timer">Time: {timer} seconds</div>
          <div class="scores">
            <h2>High Scores</h2>
            <ul>
              {#each scores as score}
                <li>Score: {score.time} seconds at {new Date(score.now).toLocaleString()}</li>
              {/each}
            </ul>
          </div>
        </Card>
    </Grid>
  </Row>

<style>
  .title {
    color: #17a6ce;
    text-align: center;
    font-size: 2.8rem;
    margin-bottom: 1.5rem;
    font-family: 'Comic Sans MS', cursive, sans-serif;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
  }

  .letters {
    font-size: 1.8rem;
    background: #fff8fa;
    padding: 1.5rem;
    border-radius: 15px;
    margin: 1.5rem 0;
    min-height: 70px;
    box-shadow: inset 0 2px 8px rgba(255, 105, 180, 0.1);
    border: 2px dashed #67d2db;
    color: #4a4a4a;
  }

  .controls {
    display: flex;
    gap: 1.2rem;
    justify-content: center;
    margin: 1.5rem 0;
  }

  .btn {
    background: linear-gradient(145deg, #17a6ce, #17a6ce);
    color: white;
    border: none;
    padding: 1rem 2rem;
    border-radius: 25px;
    cursor: pointer;
    font-size: 1.1rem;
    font-weight: bold;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(255, 105, 180, 0.3);
  }

  .btn:hover {
    background: linear-gradient(145deg, #17a6ce, #17a6ce);
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(124, 203, 231, 0.4);
  }

  .timer {
    text-align: center;
    font-size: 1.4rem;
    color: #17a6ce;
    margin: 1.2rem 0;
    font-weight: bold;
  }

  .scores {
    margin-top: 2.5rem;
    background: #fff8fa;
    padding: 1.5rem;
    border-radius: 15px;
    border: 2px solid #ffd6e6;
  }

  .scores h2 {
    color: #17a6ce;
    font-size: 1.8rem;
    margin-bottom: 1.2rem;
    text-align: center;
    font-family: 'Comic Sans MS', cursive, sans-serif;
  }

  .scores ul {
    list-style: none;
    padding: 0;
  }

  .scores li {
    background: white;
    padding: 1rem;
    margin: 0.8rem 0;
    border-radius: 12px;
    color: #4a4a4a;
    border: 1px solid #ffd6e6;
    transition: transform 0.2s ease;
  }

  .scores li:hover {
    transform: scale(1.02);
    box-shadow: 0 4px 12px rgba(255, 105, 180, 0.15);
  }

  @keyframes float {
    0% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
    100% { transform: translateY(0px); }
  }

  .title {
    animation: float 3s ease-in-out infinite;
  }
</style>


