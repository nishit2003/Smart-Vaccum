<script>
  import Login from "./components/Login.svelte";

  let loggedIn = false; // Track if user is logged in
  let user = { username: "", name: "" }; // Track user information

  let isDarkMode = false;

  // toggle theme
  const toggleTheme = () => {
    isDarkMode = !isDarkMode;
    document.documentElement.setAttribute(
      "data-theme",
      isDarkMode ? "dark" : "light"
    );
  };

  // login success handler
  const onLoginSuccess = (event) => {
    user.username = event.detail.username; // Assign username after login
    user.name = event.detail.name; // Correctly assign the name after login
    loggedIn = true;
    
    // Show welcome message
    alert(`Welcome, ${user.name}!`);
  };
</script>

<main>
  {#if !loggedIn}
    <!-- Show login form if user is not logged in -->
    <Login on:login={onLoginSuccess} />
  {:else}
    <!-- Show welcome message if user is logged in -->
    <h1>Welcome, {user.name}!</h1>
    <p>Thank you for logging in, {user.username}.</p>
  {/if}
</main>

<style>
  /* Optional styling */
  main {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 2rem;
  }
</style>
