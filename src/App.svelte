<script>
	// import { color } from './../node_modules/flowbite-svelte-icons/dist/CartPlusSolid.svelte.d.ts';
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

  <main class="mt-16">
    <div class="header-control-container">
      <!-- Hello message and control panel side by side -->
      <div class="header-text">
        <h1 class="robo-ai">Hello {user.name} !</h1>
        <h5 class="robo-ai">Thank you for being with us!</h5>
      </div>

      <!-- Control Panel in the same line as Hello message -->
      <div class="control-box">
        <ControlPanel />
      </div>
    </div>

    <div class="t-box">
      <Timer {isDarkMode} />
    </div>

    <!-- Battery status component -->
    <div class="battery-box">
      <BatteryStatus />
    </div>

    <div class="cleaning-box">
      <CleaningStatus />
    </div>
  </main>
{/if}

<style>
   /* Flexbox for aligning the header and control panel side by side */
  .header-control-container {
    display: flex;
    justify-content: flex-end; /* Space between the text and control panel */
    align-items: center; /* Vertically center-align */
    padding: 10px 20px; /* Add some padding for spacing */
    margin-left: 400px;
  }

  .header-text {
    flex: 1; /* Make the text take up more space */
  }

  .control-box {
    flex-shrink: 0; /* Prevent the control panel from shrinking */
  }

  .t-box, .battery-box, .cleaning-box {
    margin-left: 180px;
    margin-top: 20px;
  }

  h1.robo-ai {
    font-size: 3em; /* Adjust the size of the Hello text */
    margin: 0;
    color: blue
  }

  h5.robo-ai {
    margin: 0;
    font-size: 2em;
    font-weight: normal;
    color: #666; /* Softer color for the subheading */
  }
</style>
