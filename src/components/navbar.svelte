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

  import UserInfoButton from "./UserInfoButton.svelte";
  import Schedule from "./schedule.svelte";
  import History from "./History.svelte";
  import MapModal from "./map.svelte";
  import Support from "./support.svelte";

  export let user = { name: "", username: "" };
  export let isDarkMode = false;
  export let toggleTheme;

  // Reactive properties to control modals
  let showScheduleModal = false;
  let showHistoryModal = false;
  let showMapModal = false;
  let showSupportModal = false;

  // Toggle functions for each modal
  const toggleScheduleModal = () => {
    showScheduleModal = true; // Set it to true to open modal
  };

  const toggleHistoryModal = () => {
    showHistoryModal = true; // Set it to true to open modal
  };

  const toggleMapModal = () => {
    showMapModal = true; // Set it to true to open modal
  };

  const toggleSupportModal = () => {
    showSupportModal = true; // Set it to true to open modal
  };
</script>

<!-- Navbar component -->
<FlowNavbar class="fixed top-0 left-0 right-0 z-50">
  <NavBrand href="/">
    <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white" style="font-weight: bold; font-family:Georgia, 'Times New Roman', Times, serif;">
      iVaccum
    </span>
  </NavBrand>

  <div class="flex items-center md:order-2 gap-x-4" style="font-weight: bold;">
    <!-- User Info Button -->
    <UserInfoButton {user}/>

    <!-- Theme Toggle Button -->
    <button
      on:click={toggleTheme}
      class="ml-3 p-2 bg-blue-500 text-white rounded-md"
      style="background-color: {isDarkMode ? '#baf7ef' : 'navy'}; color: {isDarkMode ? 'navy' : 'ghostwhite'}; font-weight: bold;"
    >
      {isDarkMode ? "Light Mode 🌝" : "Dark Mode 🌚"}
    </button>

    <!-- Avatar and Dropdown -->
    <Avatar id="avatar-menu" src="src/assets/10337609.png" />
    <Dropdown placement="bottom" triggeredBy="#avatar-menu">
      <DropdownHeader>
        <span class="block text-sm"><strong>{user.name}</strong></span>
        <!-- <span class="block truncate text-sm font-medium">{user.username}</span> -->
      </DropdownHeader>
      
      <DropdownDivider></DropdownDivider>
    </Dropdown>
  </div>

  <!-- Schedule, History, Map, and Support Modals -->
  <Schedule bind:showScheduleModal={showScheduleModal} />
  <History bind:showHistoryModal={showHistoryModal} />
  <MapModal bind:showMapModal={showMapModal} />
  <Support bind:showSupportModal={showSupportModal} />

  <!-- Navbar Links -->
  <NavUl>
    <NavLi href="/" activeClass="active" style="font-weight: bold; font-family:Georgia, 'Times New Roman', Times, serif; color: #ff13f0;">Home/Exit</NavLi>
    <NavLi on:click={toggleScheduleModal} style="cursor: pointer; font-weight: bold; font-family:Georgia, 'Times New Roman', Times, serif; color: #ff13f0;">Schedule</NavLi>
    <NavLi on:click={toggleHistoryModal} style="cursor: pointer; font-weight: bold; font-family:Georgia, 'Times New Roman', Times, serif; color: #ff13f0;">History</NavLi>
    <NavLi on:click={toggleMapModal} style="cursor: pointer; font-weight: bold; font-family:Georgia, 'Times New Roman', Times, serif; color: #ff13f0;">Map</NavLi>
    <NavLi on:click={toggleSupportModal} style="cursor: pointer; font-weight: bold; font-family:Georgia, 'Times New Roman', Times, serif; color: #ff13f0;">Support</NavLi>
  </NavUl>
</FlowNavbar>
