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
        <div class="grid-item greeting-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <div class="header-text">

            <!-- <h1 class="robo-ai" style="color: #FF10F0;">Hello {user.name}!</h1>
            <h5 class="robo-ai" style="color: #FF10F0;">Thank you for being with us!</h5> -->

            <h1>Hello {user.name} !</h1>
            <h6 style="font-style: italic;">Thank you for being with us!</h6>

            <!-- <h1 
              class="robo-ai" 
              style="
                font-size: 2em; 
                font-weight: bold; 
                background: linear-gradient(to right, red, violet); 
                background-size: 400%; 
                -webkit-background-clip: text; 
                color: transparent; 
                animation: simpleColorWave 3s linear infinite;
              ">
              Hello {user.name}!
            </h1>

            <h5 
              class="robo-ai" 
              style="
                font-size: 1.5em; 
                font-weight: bold; 
                background: linear-gradient(to right, red, ghostwhite, magenta); 
                background-size: 400%; 
                -webkit-background-clip: text; 
                color: transparent; 
                animation: simpleColorWave 3s linear infinite;
              ">
              Thank you for being with us!
            </h5> -->


            <!-- <h1 class="robo-ai" style="color: {isDarkMode ? 'ghostwhite' : 'navy'};">
              Hello {user.name}!
            </h1>
            <h5 class="robo-ai" style="color: {isDarkMode ? 'ghostwhite' : 'navy'};">
              Thank you for being with us!
            </h5> -->

          </div>
        </div>
        <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <Timer {isDarkMode} />
        </div>
        <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <BatteryStatus />
        </div>
        <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <CleaningStatus />
        </div>
        <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
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

  /* @keyframes simpleColorWave {
  0% {
    background-position: 0%;
  }
  100% {
    background-position: 100%;
  }
} */

  /* Main content fills the viewport */
  .main-content {
    display: flex;
    flex-direction: column;
    margin-left: 11px;
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
    color: ghostwhite;
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
    /* background-color: #ff4d4d; */
    color: ghostwhite;
    padding: 20px;
    border-radius: 8px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    /* Optional shadow */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  /* Light and dark mode grid item styles for better UI view */
  .grid-item.is-light {
    background-color: aqua;
    color: navy !important;
    font-weight: bold;
    font-family: Georgia, Times, "Times New Roman", serif;
  }

  .grid-item.is-dark {
    background-color: navy;
    color: ghostwhite !important;
    font-weight: bold;
    font-family: Georgia, Times, "Times New Roman", serif;
  }

  /* Dark mode adjustments */
  [data-theme="dark"] .grid-container {
    background-color: #333;
  }

  :global([data-theme="dark"]) .grid-item,
  :global([data-theme="dark"]) .greeting-item {
    background-color: #444;
    color: #fff;
  }
</style>
