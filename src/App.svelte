<script>
  import Timer from "./components/timer.svelte";
  import Navbar from "./components/navbar.svelte";
  import "./app.css";

  let user = { username: "JohnDoe", name: "John Doe" };
  let isDarkMode = false;

  // Toggle theme
  const toggleTheme = () => {
    isDarkMode = !isDarkMode;
    document.documentElement.setAttribute(
      "data-theme",
      isDarkMode ? "dark" : "light"
    );
  };
</script>

<!-- Main app content -->
<Navbar {user} {isDarkMode} {toggleTheme} />

<main class="mt-16">
  <h1 class="robo-ai">Hello {user.name} !</h1>
  <h5 class="robo-ai">Thank you for being with us!</h5>

  <div class="t-box">
    <Timer {isDarkMode} />
  </div>
</main>

<style>
  .t-box {
    margin-left: 180px;
  }
</style>
