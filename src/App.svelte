<script>
  import "./app.css";
  import {
    Navbar,
    NavBrand,
    NavLi,
    NavUl,
    Avatar,
    Dropdown,
    DropdownItem,
    DropdownHeader,
    DropdownDivider,
  } from "flowbite-svelte";
  import Login from "./components/Login.svelte";

  let loggedIn = false; // Track if user is logged in
  let user = { username: "", name: "" }; // Track user information

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
    loggedIn = true;
    alert(`Welcome, ${user.name}!`);
  };

  const handleLogout = () => {
    loggedIn = false;
    user = { username: "", name: "" };
    alert("You have been logged out.");
  };
</script>

<!-- Navbar always on top -->
<Navbar class="fixed top-0 left-0 right-0 z-50">
  <NavBrand href="/">
    <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">iVaccum</span>
  </NavBrand>

  <div class="flex items-center md:order-2">
    {#if loggedIn}
      <Avatar id="avatar-menu" src="/images/profile-picture-3.webp"></Avatar>
      <Dropdown placement="bottom" triggeredby="#avatar-menu">
        <DropdownHeader>
          <span class="block text-sm">{user.name}</span>
          <span class="block truncate text-sm font-medium">{user.username}</span>
        </DropdownHeader>
        <DropdownItem>Dashboard</DropdownItem>
        <DropdownItem>Settings</DropdownItem>
        <DropdownDivider></DropdownDivider>
        <DropdownItem on:click="{handleLogout}">Sign out</DropdownItem>
      </Dropdown>
    {/if}

    <button on:click="{toggleTheme}" class="ml-3 p-2 bg-blue-500 text-white rounded-md">
      {isDarkMode ? "Light Mode" : "Dark Mode"}
    </button>
  </div>

  <NavUl>
    <NavLi href="/" active="{true}">Home</NavLi>
    <NavLi href="/about">About</NavLi>
    <NavLi href="/docs/components/navbar">Navbar</NavLi>
    <NavLi href="/pricing">Pricing</NavLi>
    <NavLi href="/contact">Contact</NavLi>
  </NavUl>
</Navbar>

<!-- Main content starts below the navbar -->
<main class="mt-16">
  {#if !loggedIn}
    <Login on:login="{onLoginSuccess}"></Login>
  {:else}
    <h1>Welcome, {user.name}!</h1>
    <p>Thank you for logging in, {user.username}.</p>
  {/if}
</main>
