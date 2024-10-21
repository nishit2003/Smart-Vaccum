<script>
  import { Modal, Button } from "flowbite-svelte";
  
  // Import images
  import kitchenImage from "../assets/kitchen.png";
  import livingImage from "../assets/living.png";
  import bathroomImage from "../assets/bathroom.png";
  import bedroomImage from "../assets/bedroo.png";  // Make sure the path is correct

  export let showMapModal = false;

  // Room data
  let rooms = [
    { name: "Kitchen", image: kitchenImage },
    { name: "Living Room", image: livingImage },
    { name: "Bathroom", image: bathroomImage },
    { name: "Bedroom", image: bedroomImage },
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
          <h3 class="flex items-center justify-between">
            <span>{room.name}</span>
            <Button color="red" size="xs" class="mb-2">Update</Button>
          </h3>
          <img src={room.image} alt="{room.name} Map" />
        </div>
      {/each}
    </div>
    <Button color="green" class="mt-4" on:click={addNewRoom}>Add New Room</Button>
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
</style>
