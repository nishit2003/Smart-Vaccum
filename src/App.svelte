<script>
  import Timer from "./components/timer.svelte";
  import Login from "./components/login.svelte";
  import Navbar from "./components/navbar.svelte";
  import BatteryStatus from "./components/batteryhealth.svelte";
  import CleaningStatus from "./components/cleaningstatus.svelte";
  import ControlPanel from "./components/ControlPanel.svelte";
  import "./app.css";

  let user = { username: "", name: "" };
  let isDarkMode = false;
  let isLoggedIn = false;

  const handleLogin = (event) => {
    user = event.detail;
    isLoggedIn = true;
  };

  const toggleTheme = () => {
    isDarkMode = !isDarkMode;
    document.documentElement.setAttribute(
      "data-theme",
      isDarkMode ? "dark" : "light"
    );
  };
</script>

{#if !isLoggedIn}
  <Login on:login={handleLogin} />
{:else}
  <Navbar {user} {isDarkMode} {toggleTheme} />

  <main class="main-content">
    <div class="content-wrapper">
      <div class="header-container">
        <!-- Hello message -->
        <div class="header-text">
          <h1 class="robo-ai">Hello {user.name}!</h1>
          <h5 class="robo-ai">Thank you for being with us!</h5>
        </div>
      </div>

      <!-- Grid container for components -->
      <div class="grid-container">
        <div class="grid-item">
          <Timer {isDarkMode} />
        </div>
        <div class="grid-item">
          <BatteryStatus />
        </div>
        <div class="grid-item">
          <CleaningStatus />
        </div>
        <div class="grid-item">
          <!-- Control Panel now placed here -->
          <ControlPanel />
        </div>
      </div>
    </div>
  </main>
{/if}

<style>
  /* Reset margins and paddings */
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  /* Main content fills the viewport */
  .main-content {
    display: flex;
    flex-direction: column;
    padding-top: 60px; /* Adjust according to your Navbar height */
  }

  /* Wrapper to center content */
  .content-wrapper {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    flex: 1;
    display: flex;
    flex-direction: column;
  }

  /* Header and control panel */
  .header-control-container {
    display: flex;
    justify-content: flex-end; /* Space between the text and control panel */
    align-items: center; /* Vertically center-align */
    padding: 10px 20px; /* Add some padding for spacing */
    margin-left: 400px;
  }

  .header-text {
    flex: 1;
  }

  .control-box {
    flex-shrink: 0;
  }

  h1.robo-ai {
    font-size: 3em; /* Adjust the size of the Hello text */
    margin: 0;
    color: blue;
    color: #333333; /* Darker color for visibility */
  }

  h5.robo-ai {
    margin: 0;
    font-size: 2em;
    font-weight: normal;
    color: #666;
  }

  /* Grid container styles */
  .grid-container {
    flex: 1;
    display: grid;
    grid-template-columns: 1fr 1fr; /* 2 columns */
    grid-template-rows: 1fr 1fr;    /* 2 rows */
    gap: 20px;
    padding: 20px;
    background-color: #eaeaea;
  }

  .grid-item {
    background-color: #ffffff;
    padding: 20px;
    border-radius: 8px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    /* Optional shadow */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  /* Dark mode adjustments */
  [data-theme="dark"] .header-container {
    background-color: #222;
  }

  [data-theme="dark"] .grid-container {
    background-color: #333;
  }

  [data-theme="dark"] .grid-item {
    background-color: #444;
    color: #fff;
  }
</style>
