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
      <!-- Grid container for components -->
      <div class="grid-container">
        <!-- Greeting message grid item -->
        <div class="grid-item greeting-item">
          <div class="header-text">
            <h1 class="robo-ai">Hello {user.name}!</h1>
            <h5 class="robo-ai">Thank you for being with us!</h5>
          </div>
        </div>
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

  /* Grid container styles */
  .grid-container {
    flex: 1;
    display: grid;
    grid-template-columns: 1fr 1fr; /* 2 columns */
    gap: 20px;
    padding: 20px;
    background-color: #eaeaea;
  }

  /* Make the greeting message span two columns */
  .greeting-item {
    grid-column: 1 / -1; /* Spans from column 1 to the end */
    background-color: #ffffff;
    padding: 20px;
    border-radius: 8px;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    /* Optional shadow */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
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

  h1.robo-ai {
    font-size: 2em;
    margin-bottom: 10px;
    color: #333333; /* Darker color for visibility */
  }

  h5.robo-ai {
    margin: 0;
    font-size: 1.5em;
    font-weight: normal;
    color: #666;
  }

  /* Dark mode adjustments */
  :global([data-theme="dark"]) .grid-container {
    background-color: #333;
  }

  :global([data-theme="dark"]) .grid-item,
  :global([data-theme="dark"]) .greeting-item {
    background-color: #444;
    color: #fff;
  }

  :global([data-theme="dark"]) h1.robo-ai {
    color: #fff;
  }

  :global([data-theme="dark"]) h5.robo-ai {
    color: #ddd;
  }
</style>
