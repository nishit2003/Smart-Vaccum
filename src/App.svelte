<script>
  import Timer from "./components/timer.svelte";
  import Login from "./components/login.svelte";
  import Navbar from "./components/navbar.svelte";
  import BatteryStatus from "./components/batteryhealth.svelte";
  import CleaningStatus from "./components/cleaningstatus.svelte";
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
    <h1 class="robo-ai">Hello {user.name} !</h1>
    <h5 class="robo-ai">Thank you for being with us!</h5>

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
  .t-box {
    margin-left: 180px;
  }
  .battery-box , .cleaning-box{
    margin-left: 180px;
    margin-top: 20px;
  }
</style>
