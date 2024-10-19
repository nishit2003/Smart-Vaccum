<script>
  import { Modal, Button } from "flowbite-svelte";
  export let showMapModal = false;

  // Room data
  let rooms = [
    { name: "Kitchen", image: "src/assets/kitchen.png" },
    { name: "Living Room", image: "src/assets/living.png" },
    { name: "Bathroom", image: "src/assets/bathroom.png" },
    { name: "Bedroom", image: "src/assets/bedroo.png" },
  ];

  // Function to add a new room
  const addNewRoom = () => {
    const roomName = prompt("Enter room name:");
    const roomImage = prompt("Enter image URL:");
    if (roomName && roomImage) {
      rooms = [...rooms, { name: roomName, image: roomImage }];
    }
  };
</script>

<!-- Modal for map -->
<Modal open={showMapModal} on:close={() => (showMapModal = false)} placement="center">
  <div class="modal-content">
    <h2 class="map-title">Home Maps</h2>
    <div class="map-grid">
      {#each rooms as room}
        <div class="map-item">
          <h3>{room.name} <Button color="light" size="xs" class="update-button">Update</Button></h3>
          <img src={room.image} alt="{room.name} Map" />
        </div>
      {/each}
    </div>
    <Button color="light" class="mt-4" on:click={addNewRoom}>Add New Room</Button>
    <Button color="light" class="mt-4" on:click={() => (showMapModal = false)}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 1.5rem;
    text-align: left;
  }
  .map-title {
    font-weight: bold;
    margin-bottom: 1rem;
  }
  .map-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.5rem;
  }
  .map-item {
    text-align: center;
  }
  .map-item img {
    max-width: 100%;
    height: auto;
    border: 1px solid #ccc;
    border-radius: 8px;
  }
  .update-button {
    margin-left: 0.5rem;
  }
  .add-room-button {
    position: fixed;
    bottom: 1rem;
    right: 1rem;
    z-index: 100;
  }
</style>
