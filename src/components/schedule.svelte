<script>
  import { Modal, Button } from "flowbite-svelte";
  export let showScheduleModal = false;

  // User's scheduled cleaning data
  let schedule = [
    { day: "Monday", time: "10:00 AM" },
    { day: "Wednesday", time: "3:00 PM" },
    { day: "Friday", time: "12:00 PM" },
  ];

  const toggleScheduleModal = () => {
    showScheduleModal = !showScheduleModal;
  };

  // Function to add a new schedule
  const addSchedule = () => {
    schedule = [...schedule, { day: "", time: "" }];
  };

  // Function to remove a schedule
  const removeSchedule = (index) => {
    schedule = schedule.filter((_, i) => i !== index);
  };
</script>

<!-- Modal for scheduling -->
<Modal open={showScheduleModal} on:close={toggleScheduleModal} placement="center">
  <div class="modal-content">
    <h2 class="schedule-title">Schedule Cleaning</h2>
    <div class="schedule-list">
      {#each schedule as { day, time }, index}
        <div class="schedule-item">
          <input type="text" bind:value={day} placeholder="Day" class="day-input" />
          <input type="time" bind:value={time} class="time-input" />
          <Button color="red" on:click={() => removeSchedule(index)}>Remove</Button>
        </div>
      {/each}
    </div>
    <Button color="green" class="mt-4" on:click={addSchedule}>Add Schedule</Button>
    <Button color="light" class="mt-4" on:click={toggleScheduleModal}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 1.5rem;
    text-align: left;
  }
  .schedule-title {
    font-weight: bold;
    margin-bottom: 1rem;
  }
  .schedule-list {
    margin-bottom: 1rem;
  }
  .schedule-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 0.5rem;
  }
  .day-input {
    flex: 1;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  .time-input {
    flex: 1;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
</style>
