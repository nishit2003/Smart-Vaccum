<script>
  import { Modal, Button } from "flowbite-svelte"; // Import modal from Flowbite

  export let user = { name: "", username: "" };
  let showModal = false;

  // Mock user info and device info
  // const userInfo = {
  //   name: "Nishit Grover",
  //   username: "nishit123",
  // };

  const deviceInfo = {
    deviceName: "Smart Vacuum",
    batteryStatus: "80%",
    lastCleaned: "2 hours ago",
    modelNumber: "AAXNN2342",
  };

  // Instructions on how to use the smart vacuum
  const instructions = [
    "Press the 'Start' button to begin a cleaning session.",
    "Press the 'Stop' button to stop the cleaning.",
    "Press the 'Timer' button to start a timed cleaning session.",
    "Use the 'Suction' button to adjust the vacuum power.",
    "Check the battery status on the top right of the UI.",
    "Use 'Schedule' to set a recurring cleaning time.",
    "Press 'Return to Dock' to send the vacuum back to its charging station.",
  ];

  const toggleModal = () => {
    showModal = !showModal;
  };

</script>

<!-- Button to open the modal -->
 <div class="open-modal-btn">  
  <Button on:click={toggleModal}>Show User & Device Information</Button>
</div>

<!-- Modal Window -->
<Modal open={showModal} on:close={toggleModal} placement="center">
  <div class="modal-content">
    <h1 class="info-title">User Information</h1>
    <div class="info-box">
      <p><strong>Name:</strong> {user.name}</p>
      <p><strong>Username:</strong> {user.username}</p>
    </div>
    <br />
    <h1 class="info-title">Device Information</h1>
    <div class="info-box">
      <p><strong>Device:</strong> {deviceInfo.deviceName}</p>
      <p><strong>Model Number:</strong> {deviceInfo.modelNumber}</p>
      <!-- <p><strong>Battery Status:</strong> {deviceInfo.batteryStatus}</p>
      <p><strong>Last Cleaned:</strong> {deviceInfo.lastCleaned}</p> -->
    </div>
    <br />
    <h1 class="info-title">How to Use the Smart Vacuum</h1>
    <ul class="instructions-list">
      <!-- {#each instructions as instruction}
        <li  class="instruction-item">{instruction}</li>
      {/each} -->
          <li class="instruction-item">Press the 'Start' button to begin a cleaning session.</li>
          <li class="instruction-item">Press the 'Stop' button to stop the cleaning.</li>
          <li class="instruction-item">Press the 'Timer' button to start a timed cleaning session.</li>
          <li class="instruction-item">Use the 'Suction' button to adjust the vacuum power.</li>
          <li class="instruction-item">Check the battery status on the top right of the UI.</li>
          <li class="instruction-item">Use 'Schedule' to set a recurring cleaning time.</li>
          <li class="instruction-item">Press 'Return to Dock' to send the vacuum back to its charging station.</li>
    </ul>

  <!-- <Button color="light" class="mt-4" on:click={() => (showModal = false)}>Close</Button> -->

    <!-- Close Button -->
    <!-- <div class="close-modal-btn">  
      <Button color="light" on:click={toggleModal}>Close</Button>
    </div> -->

  </div>
</Modal>

<style>
  .modal-content {
    padding: 2rem;
    text-align: center;
    background: linear-gradient(145deg, #ff4d4d, #ff4d4d);
    border-radius: 20px;
    box-shadow: 6px 6px 12px rgba(0, 0, 0, 0.2), -6px -6px 12px rgba(255, 255, 255, 0.5);
  }

  .info-title {
    font-size: 2rem;
    color: ghostwhite;
    font-weight: bold;
    margin-bottom: 1rem;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
  }

  .info-box {
    background: aqua;
    color: navy;
    padding: 1rem;
    border-radius: 15px;
    box-shadow: inset 2px 2px 8px rgba(0, 0, 0, 0.1), inset -2px -2px 8px rgba(255, 255, 255, 0.5);
    margin-bottom: 1.5rem;
  }

  /* .close-modal-btn {
    margin-top: 1rem;
  } */

  p {
    font-size: 1.2rem;
    margin: 0.5rem 0;
  }

  .instructions-list {
    list-style-type: none;
    color: navy;
    padding: 0;
    margin: 0;
    margin-bottom: 1.5rem;
  }

  .instruction-item {
    font-size: 1.1rem;
    margin-bottom: 0.7rem;
    padding: 0.7rem;
    background: aqua;
    border-radius: 10px;
    box-shadow: 3px 3px 6px rgba(0, 0, 0, 0.1), -3px -3px 6px rgba(255, 255, 255, 0.5);
    transition: transform 0.3s;
  }

  .instruction-item:hover {
    transform: translateY(-3px);
  }

  .open-modal-btn {
    background: linear-gradient(145deg);
    border-radius: 25px;
    font-weight: bold;
    font-size: 1rem;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.2), -4px -4px 8px rgba(255, 255, 255, 0.5);
    transition: all 0.3s ease;
  }

  .open-modal-btn:hover {
    background: linear-gradient(145deg, #e4e4e4, #bfbfbf);
    box-shadow: 6px 6px 12px rgba(0, 0, 0, 0.3), -6px -6px 12px rgba(255, 255, 255, 0.6);
    transform: translateY(-3px);
  }
</style>
