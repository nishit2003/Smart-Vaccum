<script>
  import Timer from './components/Timer.svelte';
  // import Login from './components/login.svelte';
  import Navbar from './components/Navbar.svelte';
  import "./app.css";

  // let loggedIn = false;
  let user = { username: "", name: "" };
  let isDarkMode = false;

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
    // loggedIn = true;
    alert(`Welcome, ${user.name}!`);
  };

  const handleLogout = () => {
    // loggedIn = false;
    user = { username: "", name: "" };
    alert("You have been logged out.");
  };
</script>

<!-- Use the Navbar component -->
<Navbar
  {user}
  {isDarkMode}
  {toggleTheme}
  {handleLogout}
/>

<!-- Main content starts below the navbar -->
<main class="mt-16">
  <!-- {#if !loggedIn} -->
    <!-- <Login on:login="{onLoginSuccess}"></Login> -->
  <!-- {:else} -->
    <h1>Welcome, {user.name}!</h1>
    <p>Thank you for logging in, {user.username}.</p>

    <Timer />
  <!-- {/if} -->
</main>
