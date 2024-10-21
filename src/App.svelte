<script>
  import Timer from "./components/timer.svelte";
  import Login from "./components/login.svelte";
  import Navbar from "./components/navbar.svelte";
  import BatteryStatus from "./components/batteryhealth.svelte";
  import CleaningStatus from "./components/cleaningstatus.svelte";
  import ControlPanel from "./components/ControlPanel.svelte";
  import Stop from "./components/stop.svelte";
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
        <div
          class="grid-item greeting-item"
          class:is-dark={isDarkMode}
          class:is-light={!isDarkMode}
        >
          <div class="header-text">
            <h1 class="greeting-header" style="color: #ff13f0; font-family:Georgia, 'Times New Roman', Times, serif; font-style: bold;">Hello {user.name}!</h1>
            <h6 class="greeting-subtext" style="color: #ff13f0; font-family:Georgia, 'Times New Roman', Times, serif; font-style: bold, italic;">Thank you for being with us!</h6>
          </div>
        </div>
        <div class="grid-item">
          <Stop />
        </div>
        <!-- <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <Timer {isDarkMode} />
        </div> -->
        <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <BatteryStatus />
        </div>
        <div class="grid-item" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
          <CleaningStatus />
        </div>
      </div>
    </div>
  </main>

  <div class="control-panel" class:is-dark={isDarkMode} class:is-light={!isDarkMode}>
    <ControlPanel />
    <Timer/>
  </div>
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
    width: 80vmin;
    height: 80vmin;
    margin: 50px auto;
    border-radius: 50%;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #ffafbd, #ffc3a0);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }

  /* Wrapper to center content */
  .content-wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  /* Grid container styles */
  .grid-container {
    display: grid;
    /* grid-template-columns: 1fr 1fr; */
    gap: 20px;
    width: 90%;
    height: 90%;
  }

  /* Greeting message styles */
  .greeting-item {
    grid-column: 1 / -1;
    text-align: center;
    padding: 20px;
    border-radius: 15px;
    background: rgba(255, 255, 255, 0.8);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }

  .greeting-header {
    font-size: 2rem;
    font-weight: bold;
    color: navy;
  }

  .greeting-subtext {
    font-size: 1rem;
    font-style: italic;
    color: #555;
  }

  /* Grid item styles */
  .grid-item {
    /* background-color: rgba(255, 255, 255, 0.8); */
    padding: 10px;
    border-radius: 35px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;
    /* box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); */
  }

  /* Light and dark mode grid item styles */
  .grid-item.is-light {
    background-color: #f0f0f0;
    color: navy;
  }

  .grid-item.is-dark {
    background-color: navy;
    color: #f0f0f0;
  }

  /* Light and dark mode grid item styles */
  .control-panel.is-light {
    background-color: #f0f0f0;
    color: navy;
  }

  /* Here is for the dark mode*/
  .control-panel.is-dark {
    background-color: navy;
    color: #f0f0f0;
  }

  /* Control panel styles */
  .control-panel {
    position: absolute;
    top: 120px; /* Adjust to add appropriate space below greeting */
    right: 20px;
    text-align: right;
    padding: 15px;
    background: #ffffff;
    border-radius: 15px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    /* max-width: 300px; */
    margin-top: 20px; /* Adds space below greeting message */
  }
</style>
