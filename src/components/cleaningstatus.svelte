<script>
  let dirtLevel = Math.floor(Math.random() * 101); // Generate random dirt level between 0 and 100

  // Function to update the dirt level periodically
  const updateDirtLevel = () => {
    dirtLevel = Math.floor(Math.random() * 101);
    console.log("Dirt level updated:", dirtLevel); // Log the dirt level
  };

  // Update dirt level every 5 seconds
  setInterval(updateDirtLevel, 5000);
</script>

<!-- Display cleaning status -->
<div class="cleaning-container">
  <div class="cleaning-visual">
    <div
      class="dirt-level"
      style="width: {dirtLevel}%; background-color: {dirtLevel > 80 ? '#f44336' : '#66bb6a'}"
    ></div>
  </div>
  <p class="cleaning-text" style="color: {dirtLevel > 80 ? '#f44336' : '#333'}">
    {dirtLevel > 80
      ? `Warning: Change dirt bag soon! Dirt level: ${dirtLevel}%`
      : `Vacuum is clean! Dirt level: ${dirtLevel}%`}
  </p>
</div>

<style>
  .cleaning-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: linear-gradient(145deg, #f5f5f5, #e0e0e0); /* Subtle gradient background */
    padding: 25px; /* Padding for better spacing */
    border-radius: 20px; /* Rounded corners */
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1); /* Softer and larger shadow */
    transition: transform 0.2s ease; /* Subtle scaling on hover */
    max-width: 450px;
  }

  .cleaning-container:hover {
    transform: scale(1.05); /* Scale up on hover */
  }

  .cleaning-visual {
    width: 420px; /* Increased width */
    height: 90px; /* Height for visual representation */
    border: 4px solid rgba(0, 0, 0, 0.2); /* Softer border */
    position: relative;
    margin-bottom: 15px; /* Increased margin */
    background-color: #f1f1f1; /* Light background for contrast */
    border-radius: 8px; /* Rounded corners */
    overflow: hidden; /* Ensure the dirt level stays within bounds */
  }

  .dirt-level {
    height: 100%;
    background-color: #66bb6a; /* Default color for clean status */
    transition: width 0.8s ease, background-color 0.8s ease; /* Smoother transitions */
    border-radius: 8px 0 0 8px; /* Rounded edges */
  }

  .cleaning-text {
    font-size: 22px; /* Font size for text */
    font-weight: 500; /* Lighter font weight for modern look */
    margin-top: 10px; /* Spacing above text */
    transition: color 0.3s ease;
  }
</style>
