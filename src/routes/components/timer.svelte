<script lang="ts">
  let elapsed = $state(0);
  let duration = $state(5);
  let interval: number;

  function start() {
    // clearInterval(interval);
    interval = setInterval(() => {
      elapsed += 0.1;
      if (elapsed > duration) {
        elapsed = duration;
        clearInterval(interval);
      }
    }, 100);
  }

  function reset() {
    elapsed = 0;
    start();
  }

  $effect(() => {
    if (!duration) return;
    start();

    return () => clearInterval(interval);
  });
</script>

<div class="container">
  <div>
    <label class="progress">
      <span>Elapsed time:</span>
      <progress value={elapsed} max={duration}></progress>
    </label>
  </div>

  <span>{elapsed.toFixed(1)}s</span>

  <label class="progress">
    <span>Duration</span>
    <input type="range" min={1} max={10} bind:value={duration} />
  </label>

  <button disabled={duration < 1} onclick={reset}>Reset</button>
</div>

<style>
  .container {
    max-width: 40rem;
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    padding: 2rem;
    background-color: rgb(1, 2, 21);
    border-radius: 1.2rem;
  }
  .progress {
    width: 100%;
    display: flex;
    gap: 5px;
    align-items: center;
    justify-content: space-between;
  }
  span {
    color: white;
    font-size: 1.2rem;
  }

  input {
    cursor: pointer;
  }
</style>
