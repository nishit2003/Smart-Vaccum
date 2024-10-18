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

<div class="box">
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
    <p class="time-remaining">Time remaining: {timeRemaining} seconds</p>
  {/if}
</div>

<style>
  /* 3D box styling with animated shadow */
  .box {
    background: linear-gradient(145deg, #ffffff, #e6e6e6);
    border-radius: 15px;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.1), -4px -4px 8px rgba(255, 255, 255, 0.5);
    padding: 20px;
    max-width: 400px;
    margin: 2em auto;
    text-align: center;
    transition: transform 0.3s ease;
  }

  .box:hover {
    transform: translateY(-5px);
    animation: shadow-color-change 5s infinite; /* Infinite animation for hover shadow */
  }

  /* Animation for changing shadow colors */
  @keyframes shadow-color-change {
    0% {
      box-shadow: 4px 4px 8px rgba(255, 0, 0, 0.5), -4px -4px 8px rgba(0, 255, 0, 0.5); /* Red & Green */
    }
    25% {
      box-shadow: 4px 4px 8px rgba(0, 0, 255, 0.5), -4px -4px 8px rgba(255, 255, 0, 0.5); /* Blue & Yellow */
    }
    50% {
      box-shadow: 4px 4px 8px rgba(255, 165, 0, 0.5), -4px -4px 8px rgba(75, 0, 130, 0.5); /* Orange & Indigo */
    }
    75% {
      box-shadow: 4px 4px 8px rgba(238, 130, 238, 0.5), -4px -4px 8px rgba(0, 255, 255, 0.5); /* Violet & Cyan */
    }
    100% {
      box-shadow: 4px 4px 8px rgba(255, 0, 0, 0.5), -4px -4px 8px rgba(0, 255, 0, 0.5); /* Back to Red & Green */
    }
  }

  /* Button styling */
  button {
    margin: 0.5em;
    padding: 0.5em 1em;
    border: none;
    border-radius: 25px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
  }

  button:hover {
    background-color: #0056b3;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.2);
  }

  /* Input field styling */
  input {
    padding: 0.5em;
    margin: 1em 0;
    border-radius: 25px;
    border: 1px solid #ccc;
    width: 100%;
    box-shadow: inset 2px 2px 4px rgba(0, 0, 0, 0.1);
  }

  /* Time remaining text styling */
  .time-remaining {
    color: black;
    font-weight: bold;
    font-size: 1.2em;
  }

  /* Centering content inside the box */
  .box p {
    margin-bottom: 1em;
    color: #333;
  }
</style>
