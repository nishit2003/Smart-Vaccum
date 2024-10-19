<script>
  import { Modal, Button } from "flowbite-svelte";
  import { onMount, afterUpdate } from "svelte";
  import Chart from "chart.js/auto";
  export let showHistoryModal = false;

  // User's scheduled cleaning data
  let schedule = [
    { day: "Monday", time: "10:00 AM" },
    { day: "Wednesday", time: "3:00 PM" },
    { day: "Friday", time: "12:00 PM" },
  ];

  let cleaningChart, usageChart;

  // Sample data for charts
  let cleaningEfficiencyData = {
    labels: ["Week 1", "Week 2", "Week 3", "Week 4"],
    datasets: [
      {
        label: "Cleaning Efficiency (%)",
        data: [85, 90, 87, 92],
        borderColor: "#4caf50",
        backgroundColor: "rgba(76, 175, 80, 0.2)",
      },
    ],
  };

  let usageData = {
    labels: ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
    datasets: [
      {
        label: "Usage (hours)",
        data: [1.2, 1.5, 0.8, 1.0, 1.6, 2.0, 1.3],
        borderColor: "#ff9800",
        backgroundColor: "rgba(255, 152, 0, 0.2)",
      },
    ],
  };

  // Initialize charts
  function initializeCharts() {
    const cleaningChartElement = document.getElementById("cleaningChart");
    if (cleaningChartElement instanceof HTMLCanvasElement) {
      const ctx1 = cleaningChartElement.getContext("2d");
      if (ctx1) {
        if (cleaningChart) cleaningChart.destroy();
        cleaningChart = new Chart(ctx1, {
          type: "line",
          data: cleaningEfficiencyData,
          options: {
            responsive: true,
            maintainAspectRatio: false,
          },
        });
      }
    }

    const usageChartElement = document.getElementById("usageChart");
    if (usageChartElement instanceof HTMLCanvasElement) {
      const ctx2 = usageChartElement.getContext("2d");
      if (ctx2) {
        if (usageChart) usageChart.destroy();
        usageChart = new Chart(ctx2, {
          type: "bar",
          data: usageData,
          options: {
            responsive: true,
            maintainAspectRatio: false,
          },
        });
      }
    }
  }

  onMount(() => {
    initializeCharts();
  });

  afterUpdate(() => {
    if (showHistoryModal) {
      initializeCharts();
    }
  });

  // Function to add a new schedule
  const addSchedule = () => {
    schedule = [...schedule, { day: "", time: "" }];
  };

  // Function to remove a schedule
  const removeSchedule = (index) => {
    schedule = schedule.filter((_, i) => i !== index);
  };
</script>

<!-- Modal for history -->
<Modal open={showHistoryModal} on:close={() => (showHistoryModal = false)} placement="center">
  <div class="modal-content">
    <h2 class="history-title">Cleaning History</h2>
    <div class="schedule-list">
      {#each schedule as { day, time }, index}
        <div class="schedule-item">
          <input type="text" bind:value={schedule[index].day} placeholder="Day" class="day-input" />
          <input type="time" bind:value={schedule[index].time} class="time-input" />
          <Button color="red" on:click={() => removeSchedule(index)}>Remove</Button>
        </div>
      {/each}
    </div>
    <div class="chart-container">
      <h3>Cleaning Efficiency Over Weeks</h3>
      <canvas id="cleaningChart"></canvas>
    </div>
    <div class="chart-container">
      <h3>Weekly Usage Hours</h3>
      <canvas id="usageChart"></canvas>
    </div>
    
    <Button color="light" class="mt-4" on:click={() => (showHistoryModal = false)}>Close</Button>
  </div>
</Modal>

<style>
  .modal-content {
    padding: 1.5rem;
    text-align: left;
  }
  /* .schedule-title {
    font-weight: bold;
    margin-bottom: 1rem;
  } */
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
  .chart-container {
    margin-bottom: 2rem;
    height: 300px;
  }
  canvas {
    width: 100%;
    height: 100%;
  }
</style>
