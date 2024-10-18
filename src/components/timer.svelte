<script>
  import { onMount } from 'svelte';
  export let askToStart = false;
  let timerStarted = false;
  let timeInput = 0;
  let timeRemaining = 0;
  let timerInterval;

  const startTimer = () => {
    if (timeInput > 0) {
      timeRemaining = timeInput;
      timerStarted = true;
      timerInterval = setInterval(() => {
        if (timeRemaining > 0) {
          timeRemaining -= 1;
        } else {
          clearInterval(timerInterval);
          alert('Time is up!');
          timerStarted = false;
        }
      }, 1000);
    }
  };

  const handleUserResponse = (response) => {
    askToStart = response;
    if (askToStart) {
      timeInput = 0; // Reset input
    }
  };

  onMount(() => {
    // Reset any intervals when the component is destroyed
    return () => clearInterval(timerInterval);
  });
</script>

<div>
  {#if !askToStart && !timerStarted}
    <p>Do you want to start the timer?</p>
    <button on:click={() => handleUserResponse(true)}>Yes</button>
    <button on:click={() => handleUserResponse(false)}>No</button>
  {/if}

  {#if askToStart && !timerStarted}
    <p>Enter the time for the timer (in seconds):</p>
    <input type="number" bind:value={timeInput} min="1" />
    <button on:click={startTimer}>Start Timer</button>
  {/if}

  {#if timerStarted}
    <p>Time remaining: {timeRemaining} seconds</p>
  {/if}
</div>

<style>
  div {
    text-align: center;
    margin-top: 2em;
  }
  button {
    margin: 0.5em;
  }
</style>
