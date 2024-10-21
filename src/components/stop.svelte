<script>
  let isRunning = false;

  // Functions for Start/Stop
  const start = () => {
    isRunning = true;
    console.log("Vacuum started!");
  };

  const stop = () => {
    isRunning = false;
    console.log("Vacuum stopped!");
  };
</script>

<!-- Simple Control panel with Start and Stop buttons -->
<div class="simple-control-panel">
  <button class="btn start-btn" on:click={start} disabled={isRunning}>
    Start
  </button>
  <button class="btn stop-btn" on:click={stop} disabled={!isRunning}>
    Stop
  </button>
</div>

<style>
  /* body {
    font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
    color: #333;
  } */

  .simple-control-panel {
    display: flex;
    justify-content: center;
    gap: 20px;
    padding: 20px;
    background: linear-gradient(145deg, #e0e0e0, #f0f0f0);
    border-radius: 25px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
    max-width: 400px;
    /* margin: 20px auto; */
  }

  .btn {
    padding: 15px 30px;
    font-size: 26px;
    font-weight: bold;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    background: linear-gradient(135deg, #6dd5ed, #2193b0);
    color: white;
  }

  .btn:disabled {
    cursor: not-allowed;
    opacity: 0.6;
  }

  .start-btn {
    background: linear-gradient(135deg, #a8e063, #56ab2f); /* Green for start */
  }

  .stop-btn {
    background: linear-gradient(135deg, #f85032, #e73827); /* Red for stop */
  }

  .btn:hover:not(:disabled) {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  .btn:active {
    transform: translateY(0);
  }

  /* Media Query for responsiveness */
  @media (max-width: 600px) {
    .simple-control-panel {
      flex-direction: column;
      gap: 15px;
    }
    .btn {
      width: 100%;
    }
  }
</style>
