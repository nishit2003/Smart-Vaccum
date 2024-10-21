<script>
  let isRunning = false;
  let showModal = false;
  let currentLocation = { x: 50, y: 50 }; // Random location inside the house outline

  // Functions for Start/Stop/Dock
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

  // Function to show the location modal
  const showLocation = () => {
    // Simulate a random location inside the house
    currentLocation.x = Math.random() * 100;
    currentLocation.y = Math.random() * 100;
    showModal = true;
  };

  const closeModal = () => {
    showModal = false;
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
  <button class="btn dock-btn" on:click={returnToDock}> Return to Dock </button>
  <button class="btn location-btn" on:click={showLocation}>
    Show Location
  </button>
</div>

<!-- Modal for Location -->
{#if showModal}
  <div class="modal-overlay" on:click={closeModal}>
    <div class="modal" on:click|stopPropagation>
      <h3>Your Vacuum's Current Location</h3>
      <div class="house-outline">
        <!-- Enhanced SVG Outline of House -->
        <svg viewBox="0 0 100 100" class="house-svg">
          <!-- Main outer walls of the house -->
          <rect
            x="5"
            y="5"
            width="90"
            height="90"
            stroke="black"
            fill="none"
            stroke-width="2"
          />

          <!-- Interior walls (rooms or partitions) -->
          <line
            x1="5"
            y1="35"
            x2="95"
            y2="35"
            stroke="black"
            stroke-width="1.5"
          />
          <line
            x1="35"
            y1="5"
            x2="35"
            y2="95"
            stroke="black"
            stroke-width="1.5"
          />
          <line
            x1="5"
            y1="70"
            x2="65"
            y2="70"
            stroke="black"
            stroke-width="1.5"
          />
          <line
            x1="65"
            y1="70"
            x2="65"
            y2="95"
            stroke="black"
            stroke-width="1.5"
          />

          <!-- Door openings (gaps in walls) -->
          <line
            x1="50"
            y1="35"
            x2="50"
            y2="45"
            stroke="black"
            stroke-width="1.5"
            stroke-dasharray="4"
          />
          <line
            x1="35"
            y1="55"
            x2="45"
            y2="55"
            stroke="black"
            stroke-width="1.5"
            stroke-dasharray="4"
          />

          <!-- Simulated random location marker inside the house -->
          <circle
            cx={currentLocation.x}
            cy={currentLocation.y}
            r="3"
            fill="red"
          />
        </svg>
      </div>
      <button class="btn close-btn" on:click={closeModal}>Close</button>
    </div>
  </div>
{/if}

<style>
  body {
    font-family: "Poppins", sans-serif;
    background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
    color: #333;
  }

  .control-panel {
    display: flex;
    justify-content: center;
    gap: 10px;
    padding: 10px;
    background: linear-gradient(145deg, #e0e0e0, #f0f0f0);
    border-radius: 25px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
    max-width: 1000px;
    margin: 40px auto;
  }

  .btn {
    padding: 15px 30px;
    font-size: 16px;
    font-weight: bold;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition:
      transform 0.3s ease,
      box-shadow 0.3s ease;
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

  .dock-btn {
    background: linear-gradient(135deg, #36d1dc, #5b86e5); /* Blue for dock */
  }

  .location-btn {
    background: linear-gradient(
      135deg,
      #f7971e,
      #ffd200
    ); /* Orange for show location */
  }

  .btn:hover:not(:disabled) {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  .btn:active {
    transform: translateY(0);
  }

  /* Modal Styles */
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #ffffff;
    padding: 30px;
    border-radius: 20px;
    max-width: 450px;
    width: 90%;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
    text-align: center;
  }

  .house-outline {
    margin: 30px 0;
  }

  .house-svg {
    width: 100%; /* Full width */
    height: auto;
  }

  .close-btn {
    background: linear-gradient(135deg, #f85032, #e73827);
    color: white;
    padding: 10px 25px;
    border-radius: 50px;
    cursor: pointer;
    transition: transform 0.2s ease;
  }

  .close-btn:hover {
    transform: translateY(-3px);
  }

  /* Media Query for responsiveness */
</style>
