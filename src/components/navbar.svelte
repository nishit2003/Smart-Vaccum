<script>
  import {
    Navbar as FlowNavbar,
    NavBrand,
    NavLi,
    NavUl,
    Avatar,
    Dropdown,
    DropdownItem,
    DropdownHeader,
    DropdownDivider,
  } from "flowbite-svelte";

  export let loggedIn = false;
  export let user = { username: "", name: "" };
  export let isDarkMode = false;
  export let toggleTheme;
  export let handleLogout;
</script>

<!-- Navbar component -->
<FlowNavbar class="fixed top-0 left-0 right-0 z-50">
  <NavBrand href="/">
    <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">iVaccum</span>
  </NavBrand>

  <div class="flex items-center md:order-2">
    {#if loggedIn}
      <Avatar id="avatar-menu" src="/images/profile-picture-3.webp"></Avatar>
      <Dropdown placement="bottom" trigger="click">
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
    <NavLi href="/" activeClass="active">Home</NavLi>
    <NavLi href="/about">About</NavLi>
    <NavLi href="/docs/components/navbar">Navbar</NavLi>
    <NavLi href="/pricing">Pricing</NavLi>
    <NavLi href="/contact">Contact</NavLi>
  </NavUl>
</FlowNavbar>
