<script>
  let batteryLevel = Math.floor(Math.random() * 101); // Generate random battery level between 0 and 100

  // Function to generate new random battery level periodically
  const updateBatteryStatus = () => {
    batteryLevel = Math.floor(Math.random() * 101);
    console.log("Battery level updated:", batteryLevel); // Log the battery level
  };

  // Update battery status every 5 seconds
  // setInterval(updateBatteryStatus, 5000);
</script>

<!-- Display battery status -->
<div class="battery-container">
  <p class="battery-text" style="color: {batteryLevel < 20 ? '#f44336' : '#333'}">
    {batteryLevel < 20
      ? `Warning: Charge Soon. Battery about to die: ${batteryLevel}%`
      : `Vaccum Battery: ${batteryLevel}%`}
  </p>
  <div class="battery-visual">
    <div
      class="battery-level"
      style="width: {batteryLevel}%; background-color: {batteryLevel < 20 ? '#f44336' : '#66bb6a'}"
    ></div>
  </div>
  
</div>

<style>
  .battery-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    background: linear-gradient(145deg, #f5f5f5, #e0e0e0); /* Subtle gradient background */
    padding: 25px; /* Increased padding for better spacing */
    border-radius: 20px; /* Larger rounded corners */
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1); /* Softer and larger shadow */
    transition: transform 0.2s ease; /* Subtle scaling on hover */
    max-width: 450px;
  }

  .battery-container:hover {
    transform: scale(1.05); /* Scale up on hover */
  }

  .battery-visual {
    width: 400px; /* Increased width */
    height: 50px; /* Increased height */
    border: 4px solid rgba(0, 0, 0, 0.2); /* Softer border */
    position: relative;
    margin-bottom: 15px; /* Increased margin */
    background-color: #f1f1f1; /* Light background for contrast */
    border-radius: 8px; /* More rounded corners */
    overflow: hidden; /* Ensure the battery level stays within bounds */
  }

  .battery-visual::after {
    content: '';
    width: 25px; /* Increased size of the battery terminal */
    height: 35px; /* Increased height */
    position: absolute;
    top: 50%;
    right: -27px; /* Increased distance from battery */
    background-color: rgba(0, 0, 0, 0.2); /* Softer color */
    transform: translateY(-50%);
    border-radius: 4px; /* More rounded edges */
  }

  .battery-level {
    height: 100%;
    background-color: #66bb6a; /* Default color for the battery */
    transition: width 0.8s ease, background-color 0.8s ease; /* Smoother and slower transition */
    border-radius: 8px 0 0 8px; /* Rounded edges for the battery fill */
  }

  .battery-text {
    font-size: 22px; /* Slightly larger text */
    font-weight: 500; /* Slightly lighter font weight for a modern look */
    color: #333; /* Softer text color */
    margin-top: 10px; /* Add a bit of space above the text */
    transition: color 0.3s ease;
  }
</style>
