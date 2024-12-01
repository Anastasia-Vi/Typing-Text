<script>
  import { Card, Grid, Row } from "$lib/ui/Grid";
  import { onDestroy } from "svelte";
  import { browser } from "$app/environment";
  let text = "Anastasia";
  let letters = $state(text.toLowerCase().split(''));
  let started = $state(false);
  let timer = $state(0);
  let intervalId;
  let scores = $state(browser ? JSON.parse(localStorage.getItem('typingScores')) || [] : []);
  let input = $state('');
  let guessesText = $state([]);
  $effect(() => {
    if (input.length > 0) {
      if (input.length === 1) {
        start_timer();
      }
      on_key_up(input[input.length - 1]);
    }
  })
  function on_key_up(letter) {
    let key = letter.toLowerCase();
    if (started === false) {
      return;
    } 
    if (key === letters[0]) {
    //This is code check if the key pressed is the first letter of the array and if it is, it removes it from the array
      guessesText = [...guessesText, key];
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
  function start_timer(){
    if(intervalId) clearInterval(intervalId);
    started = true;
    timer = 0;
    intervalId = setInterval(() => {//setInterval is a function that calls a function repeatedly at specified intervals
      timer = timer + 10;
    }, 10);
  }
  function restart(){
    letters = text.toLowerCase().split('');
    guessesText = []; 
    input = '';
    timer = 0;
    clearInterval(intervalId);
  }
  function on_key_down(event){
    event.preventDefault();
    if(!event.key) return;
    input = input + event.key;
    if (input.length > 0) {
      if (input.length === 1) {
        start_timer();
      }
      on_key_up(input[input.length - 1]);
    }
  }
  // Clean up interval when component is destroyed
  onDestroy(() => {
    if (intervalId) clearInterval(intervalId);
  });

</script>

 <svelte:window 
 on:keydown={on_key_down}/>


 <div class="image">
  <Row noMargin>
    <Grid>
        <Card col={12}>
          <div class="container">
            <h1 class="title">Speed Typing Test</h1>
            <div class="letters">
              <span class="guesses">{guessesText.join('')}</span>{letters.join('')}
            </div>
            <input type="text" onbeforeinput={(event)=>{
              event.preventDefault();
            }}
            bind:value={input} placeholder="Start typing to begin"/>
            <div class="controls">
              <button class="btn" on:click={restart}>Restart</button>
            </div>
            <div class="timer">Time: {timer}ms</div>
            <div class="scores">
              <h2>High Scores</h2>
              <ul>
                {#each scores as score}
                  <li>
                    <span>Score: {score.time}ms at {new Date(score.now).toLocaleString()}</span>
                    <button class="delete-btn" on:click={() => {
                      scores = scores.filter(i => i !== score);
                    }}>
                      <span class="material-icons">delete</span>
                    </button>
                  </li>
                {/each}
              </ul>
            </div>
          </div>
        </Card>
    </Grid>
  </Row>

 </div>
<style>
.guesses{
  color: #2de73a;
}

  .image {
    background-image: url('/photo1.png');
    background-size: cover;
    background-position: center;
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
    min-height: 90vh;
  }

  .title {
    color: #f8f9fa;
    text-align: center;
    font-size: 3.5rem;
    margin-bottom: 2.5rem;
    font-family: 'Inter', sans-serif;
    text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
    font-weight: 700;
  }

  .letters {
    font-size: 2.2rem;
    background: rgba(255, 255, 255, 0.85);
    border-radius: 16px;
    margin: 2rem 0;
    min-height: 100px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
    color: #2d3436;
    letter-spacing: 1px;
    backdrop-filter: blur(8px);
    text-align: center;
    padding: 0.25rem;
    line-height: 100px;
  }

  input {
    width: 100%;
    padding: 1.2rem;
    border: 2px solid rgba(255, 255, 255, 0.3);
    border-radius: 12px;
    background: rgba(255, 255, 255, 0.8);
    font-size: 1.2rem;
    margin: 1.5rem 0;
    color: #2d3436;
    backdrop-filter: blur(8px);
  }

  input:focus {
    outline: none;
    border-color: rgba(255, 255, 255, 0.5);
    background: rgba(255, 255, 255, 0.9);
  }
  .controls{
    display: flex;
    justify-content: center;
  }
  .btn {
    background: rgba(45, 52, 54, 0.85);
    color: #fff;
    border: none;
    padding: 1.2rem 3rem;
    border-radius: 12px;
    cursor: pointer;
    font-size: 1.2rem;
    font-weight: 600;
    transition: all 0.3s ease;
    backdrop-filter: blur(8px);
    
  }

  .btn:hover {
    background: rgba(45, 52, 54, 0.95);
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
  }

  .timer {
    text-align: center;
    font-size: 2rem;
    color: #f8f9fa;
    margin: 2rem 0;
    font-weight: 700;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    letter-spacing: 1px;
  }

  .scores {
    background: rgba(255, 255, 255, 0.85);
    padding: 2.5rem;
    border-radius: 16px;
    backdrop-filter: blur(8px);
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
  }

  .scores h2 {
    color: #2d3436;
    font-size: 2.2rem;
    margin-bottom: 2rem;
    text-align: center;
    font-family: 'Inter', sans-serif;
    font-weight: 700;
  }

  .scores ul {
    list-style: none;
    padding: 0;
    gap: 1.2rem;
    display: flex;
    flex-direction: column;
  }

  .scores li {
    background: rgba(255, 255, 255, 0.9);
    padding: 1.4rem;
    border-radius: 12px;
    color: #2d3436;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
  }

  .scores li:hover {
    transform: translateX(8px);
    background: rgba(255, 255, 255, 0.95);
    box-shadow: 0 6px 16px rgba(0, 0, 0, 0.1);
  }

  .delete-btn {
    background: none;
    border: none;
    color: #e74c3c;
    cursor: pointer;
    padding: 0.8rem;
    border-radius: 50%;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .delete-btn:hover {
    background: rgba(231, 76, 60, 0.1);
    transform: scale(1.1);
  }

  @media (min-width: 768px) {
    input {
      display: none;
    }
  }
</style>


