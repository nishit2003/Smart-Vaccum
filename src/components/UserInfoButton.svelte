<script>
  import { Modal, Button } from "flowbite-svelte"; // Import modal from Flowbite

  let showModal = false;

  // Mock user info and device info
  const userInfo = {
    name: "Nishit Grover",
    username: "nishit123",
  };

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
<Button on:click={toggleModal}>Show User & Device Info</Button>

<!-- Modal Window -->
<Modal open={showModal} on:close={toggleModal} placement="center">
  <div class="modal-content">
    <h2 class="info-title">User Info</h2>
    <p><strong>Name:</strong> {userInfo.name}</p>
    <p><strong>Username:</strong> {userInfo.username}</p>
    <br />
    <h2 class="info-title">Device Info</h2>
    <p><strong>Device:</strong> {deviceInfo.deviceName}</p>
    <p><strong>Model Number:</strong> {deviceInfo.modelNumber}</p>
    <!-- <p><strong>Battery Status:</strong> {deviceInfo.batteryStatus}</p>
    <p><strong>Last Cleaned:</strong> {deviceInfo.lastCleaned}</p> -->
    <br />
    <h2 class="info-title">How to Use the Smart Vacuum</h2>
    <ul>
      {#each instructions as instruction}
        <li>{instruction}</li>
      {/each}
    </ul>

    <!-- Close Button -->
    <Button class="mt-4" color="light" on:click={toggleModal}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 1.5rem;
    text-align: left;
  }
  .info-title {
    font-weight: bold;
    margin-bottom: 0.5rem;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  ul li {
    margin-bottom: 0.5rem;
  }
</style>
