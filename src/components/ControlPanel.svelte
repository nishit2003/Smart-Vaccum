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
  <button class="btn dock-btn" on:click={returnToDock}>
    Return to Dock
  </button>
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
          <rect x="5" y="5" width="90" height="90" stroke="black" fill="none" stroke-width="2" />
          
          <!-- Interior walls (rooms or partitions) -->
          <line x1="5" y1="35" x2="95" y2="35" stroke="black" stroke-width="1.5" />
          <line x1="35" y1="5" x2="35" y2="95" stroke="black" stroke-width="1.5" />
          <line x1="5" y1="70" x2="65" y2="70" stroke="black" stroke-width="1.5" />
          <line x1="65" y1="70" x2="65" y2="95" stroke="black" stroke-width="1.5" />

          <!-- Door openings (gaps in walls) -->
          <line x1="50" y1="35" x2="50" y2="45" stroke="black" stroke-width="1.5" stroke-dasharray="4" />
          <line x1="35" y1="55" x2="45" y2="55" stroke="black" stroke-width="1.5" stroke-dasharray="4" />

          <!-- Simulated random location marker inside the house -->
          <circle cx={currentLocation.x} cy={currentLocation.y} r="3" fill="red" />
        </svg>
      </div>
      <button class="btn close-btn" on:click={closeModal}>Close</button>
    </div>
  </div>
{/if}

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

  .location-btn {
    background-color: #ff9800; /* Orange for show location */
    color: white;
  }

  .btn:hover:not(:disabled) {
    transform: scale(1.05);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  }

  .btn:active {
    transform: scale(0.95);
  }

  /* Modal Styles */
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: white;
    padding: 20px;
    border-radius: 10px;
    max-width: 400px;
    width: 90%;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    text-align: center;
  }

  .house-outline {
    margin: 20px 0;
  }

  .house-svg {
    width: 100%; /* Full width */
    height: 300px; /* Fixed height for the house outline */
  }

  .close-btn {
    background-color: #f44336;
    color: white;
    padding: 10px 20px;
    border-radius: 5px;
    cursor: pointer;
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

    .house-svg {
      height: 200px; /* Smaller house outline for small screens */
    }
  }
</style>
