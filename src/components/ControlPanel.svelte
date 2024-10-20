<script>
  let isRunning = false;

  const start = () => {
    isRunning = true;
    console.log("Vacuum started!");
  };

  const stop = () => {
    isRunning = false;
    console.log("Vacuum stopped!");
  };

  const returnToDock = () => {
    console.log("Returning to dock...");
  };
</script>

<!-- Control panel with buttons -->
<div class="control-panel">
  <button class="btn start-btn" on:click={start} disabled={isRunning}>
    Start
  </button>
  <button class="btn stop-btn" on:click={stop} disabled={!isRunning}>
    Stop
  </button>
  <button class="btn dock-btn" on:click={returnToDock}>
    Return to Dock
  </button>
</div>

<style>
  .control-panel {
    display: flex;
    justify-content: center;
    gap: 20px;
    padding: 20px;
    background: linear-gradient(145deg, #ffffff, #f0f0f0);
    border-radius: 15px;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
    max-width: 500px;
    margin: auto;
  }

  .btn {
    padding: 15px 25px;
    font-size: 16px;
    font-weight: bold;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }

  .btn:disabled {
    cursor: not-allowed;
    opacity: 0.5;
  }

  .start-btn {
    background-color: #4caf50; /* Green for start */
    color: white;
  }

  .stop-btn {
    background-color: #f44336; /* Red for stop */
    color: white;
  }

  .dock-btn {
    background-color: #2196f3; /* Blue for dock */
    color: white;
  }

  .btn:hover:not(:disabled) {
    transform: scale(1.05);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  }

  .btn:active {
    transform: scale(0.95);
  }

  /* Media Query for responsiveness */
  @media (max-width: 600px) {
    .control-panel {
      flex-direction: column;
      gap: 15px;
    }
    .btn {
      width: 100%;
    }
  }
</style>
