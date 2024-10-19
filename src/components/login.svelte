  <script>
    import { createEventDispatcher } from 'svelte';
    
    let firstName = '';
    let lastName = '';
    const dispatch = createEventDispatcher();
    
    const handleLogin = () => {
      if (firstName && lastName) {
        // Dispatch login event with user details
        dispatch('login', { name: `${firstName} ${lastName}`, username: `${firstName.toLowerCase()}${lastName.toLowerCase()}` });
      } else {
        alert('Please enter both your First Name and Last Name.');
      }
    };
  </script>

  <div class="box">
    <!-- Login Box -->
    <h2 class="h2-class">Welcome RoboAI's Loyal Member!</h2>
    <input type="text" bind:value={firstName} placeholder="Enter Your First Name" />
    <input type="text" bind:value={lastName} placeholder="Enter Your Last Name" />
    <button on:click={handleLogin}>RoboAi: Smart-Clean Living Starts Here...</button>
  </div>
  
  <style>
    .h2-class {
        font-weight:bold;
    }
    /* Shared 3D box styling with animated shadow for both timer and login box */
    .box {
      background: linear-gradient(145deg, #ffffff, #e6e6e6);
      border-radius: 15px;
      box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.1), -4px -4px 8px rgba(255, 255, 255, 0.5);
      padding: 20px;
      max-width: 400px;
      margin: 2em auto;
      margin-left: 250px;
      text-align: center;
      transition: transform 0.3s ease;
    }
  
    .box:hover {
      transform: translateY(-5px);
      animation: shadow-color-change 5s infinite;
    }
  
    /* Animation for changing shadow colors */
    @keyframes shadow-color-change {
      0% {
        box-shadow: 4px 4px 8px rgba(255, 0, 0, 0.5), -4px -4px 8px rgba(0, 255, 0, 0.5);
      }
      25% {
        box-shadow: 4px 4px 8px rgba(0, 0, 255, 0.5), -4px -4px 8px rgba(255, 255, 0, 0.5);
      }
      50% {
        box-shadow: 4px 4px 8px rgba(255, 165, 0, 0.5), -4px -4px 8px rgba(75, 0, 130, 0.5);
      }
      75% {
        box-shadow: 4px 4px 8px rgba(238, 130, 238, 0.5), -4px -4px 8px rgba(0, 255, 255, 0.5);
      }
      100% {
        box-shadow: 4px 4px 8px rgba(255, 0, 0, 0.5), -4px -4px 8px rgba(0, 255, 0, 0.5);
      }
    }
  
    /* Button styling */
    button {
      margin: 0.5em;
      padding: 0.5em 1em;
      border: none;
      border-radius: 25px;
      background-color: #007bff;
      color: white;
      cursor: pointer;
      box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
    }
  
    button:hover {
      background-color: #0056b3;
      box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.2);
    }
  
    /* Input field styling */
    input {
      padding: 0.5em;
      margin: 1em 0;
      border-radius: 25px;
      border: 1px solid #ccc;
      width: 100%;
      box-shadow: inset 2px 2px 4px rgba(0, 0, 0, 0.1);
    }
  </style>