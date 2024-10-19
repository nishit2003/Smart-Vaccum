<script>
  import Timer from "./components/Timer.svelte";
  import Login from "./components/Login.svelte";
  import Navbar from "./components/navbar.svelte";
  import "./app.css";

  let user = { username: "", name: "" };
  let isDarkMode = false;
  let isLoggedIn = false;

  // Handle login and update user information
  const handleLogin = (event) => {
    user = event.detail; // Update user details from the login component
    isLoggedIn = true; // Set the login state to true
  };

  // Toggle theme
  const toggleTheme = () => {
    isDarkMode = !isDarkMode;
    document.documentElement.setAttribute(
      "data-theme",
      isDarkMode ? "dark" : "light"
    );
  };
</script>

{#if !isLoggedIn}
  <!-- Login Component -->
  <Login on:login={handleLogin} />
{:else}
  <!-- Main app content after login -->
  <Navbar {user} {isDarkMode} {toggleTheme} />

  <main class="mt-16">
    <h1 class="robo-ai">Hello {user.name} !</h1>
    <h5 class="robo-ai">Thank you for being with us!</h5>

    <div class="t-box">
      <Timer {isDarkMode} />
    </div>
  </main>
{/if}

<style>
  .t-box {
    margin-left: 180px;
  }
</style>
