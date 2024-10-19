<script>
  import Timer from "./components/timer.svelte";
  import Login from "./components/login.svelte";
  import Navbar from "./components/navbar.svelte";
  import "./app.css";
  let user = { username: "", name: "" };
  let isDarkMode = false;
  let loggedIn = false; // Track whether the user is logged in

  // Toggle theme
  const toggleTheme = () => {
    isDarkMode = !isDarkMode;
    document.documentElement.setAttribute(
      "data-theme",
      isDarkMode ? "dark" : "light"
    );
  };

  // Login success handler
  const onLoginSuccess = (event) => {
    user.username = event.detail.username;
    user.name = event.detail.name;
    loggedIn = true; // Set loggedIn to true when login succeeds
  };

  const handleLogout = () => {
    loggedIn = false; // Set loggedIn to false when logged out
    user = { username: "", name: "" };
    alert("You have been logged out.");
  };
</script>

<!-- Conditionally render the Login page or the main app content -->
{#if !loggedIn}
  <!-- Display login box if user is not logged in -->
  <div class="login-container">
    <Login on:login={onLoginSuccess} />
  </div>
{:else}
  <!-- Show the main app content after the user logs in -->
  <Navbar {user} {isDarkMode} {toggleTheme} {handleLogout} />

  <main class="mt-16">
    <h1 class="robo-ai">Hello {user.name} {user.username} !</h1>
    <h5 class="robo-ai">Thank you for logging in!</h5>

    <div class="t-box">
      <Timer {isDarkMode} />
    </div>
  </main>
{/if}

<style>
  .t-box {
    margin-left: 180px;
  }
  /* Position the login box beside the existing app when both are shown */
  .login-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh; /* Full height */
  }
</style>
