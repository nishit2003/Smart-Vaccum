<script>
    import { createEventDispatcher } from 'svelte';
    
    let username = '';
    let password = '';
    let firstName = '';
    let lastName = '';
    let homeType = '';
    let numOfRooms = 1;
    let isLogin = true;  // Toggle between login and sign-up
    const dispatch = createEventDispatcher(); // Create dispatcher to send login event

    // Function to handle login
    const handleLogin = () => {
        const storedUser = JSON.parse(localStorage.getItem(username));
        
        if (storedUser && storedUser.password === password) {
            alert(`Welcome back, ${storedUser.firstName} ${storedUser.lastName}!`);
            dispatch('login', { username, firstName: storedUser.firstName, lastName: storedUser.lastName });
        } else {
            alert('Invalid username or password.');
        }
    };

    // Function to handle sign-up
    const handleSignUp = () => {
        const storedUser = JSON.parse(localStorage.getItem(username));

        if (storedUser) {
            alert('User already exists. Please login.');
        } else {
            const newUser = {
                username,
                password,
                firstName,
                lastName,
                homeType,
                numOfRooms
            };
            localStorage.setItem(username, JSON.stringify(newUser));
            alert('Account created! Please login.');
            isLogin = true;  // Switch back to login mode
        }
    };

    // Function to handle form submission based on mode
    const handleSubmit = () => {
        if (isLogin) {
            handleLogin();
        } else {
            handleSignUp();
        }
    };

    // Toggle between Login and Sign-Up
    const toggleMode = () => {
        isLogin = !isLogin;
    };
</script>

<style>
    .login-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: auto;
        background: linear-gradient(to bottom right, #f0f4f8, #d9e8f5); /* Light and modern gradient */
        font-family: 'Poppins', sans-serif;
        padding: 2rem;
    }

    .header {
        font-size: 2.2rem;
        color: #00509e;
        margin-bottom: 1.5rem;
        text-align: center;
        font-weight: bold;
    }

    .login-box {
        padding: 2rem;
        border-radius: 15px;
        box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
        background-color: white;
        max-width: 400px;
        width: 100%;
        text-align: center;
        transition: box-shadow 0.3s ease-in-out;
    }

    .login-box:hover {
        box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
    }

    input, select {
        margin: 0.75rem 0;
        padding: 0.8rem;
        width: 100%;
        border-radius: 8px;
        border: 1px solid #ddd;
        font-size: 1rem;
        transition: border-color 0.3s ease-in-out;
    }

    input:focus, select:focus {
        border-color: #007bff;
        outline: none;
    }

    button {
        margin-top: 1.5rem;
        padding: 0.9rem;
        border: none;
        border-radius: 8px;
        background-color: #007bff;
        color: white;
        font-size: 1.1rem;
        cursor: pointer;
        width: 100%;
        transition: background-color 0.3s ease-in-out;
    }

    button:hover {
        background-color: #0056b3;
    }

    .toggle-button {
        margin-top: 1rem;
        background-color: transparent;
        color: #007bff;
        border: none;
        cursor: pointer;
        font-size: 0.9rem;
        transition: color 0.3s ease-in-out;
    }

    .toggle-button:hover {
        color: #0056b3;
    }

    .icon {
        font-size: 5rem;
        color: #00509e;
        margin-bottom: 1.5rem;
    }

    .input-label {
        text-align: left;
        font-weight: 500;
        color: #333;
    }

    @media (max-width: 600px) {
        .login-box {
            padding: 1.5rem;
        }

        .header {
            font-size: 1.8rem;
        }

        .icon {
            font-size: 3.5rem;
        }
    }
</style>

<div class="login-container">
    <i class="icon">🧹</i> <!-- Smart vacuum icon -->
    <div class="header">{isLogin ? 'Smart Vacuum Login' : 'Create Your Account'}</div>

    <div class="login-box">
        <h2>{isLogin ? 'Login' : 'Sign Up'}</h2>

        <div class="input-label">Username</div>
        <input type="text" bind:value={username} placeholder="Enter your username" />

        <div class="input-label">Password</div>
        <input type="password" bind:value={password} placeholder="Enter your password" />

        {#if !isLogin}
            <!-- Additional fields for sign-up -->
            <div class="input-label">First Name</div>
            <input type="text" bind:value={firstName} placeholder="Enter your first name" />

            <div class="input-label">Last Name</div>
            <input type="text" bind:value={lastName} placeholder="Enter your last name" />

            <div class="input-label">Home Type</div>
            <input type="text" bind:value={homeType} placeholder="Apartment, House, etc." />

            <div class="input-label">Number of Rooms</div>
            <input type="number" bind:value={numOfRooms} min="1" placeholder="Number of rooms" />
        {/if}

        <button on:click={handleSubmit}>{isLogin ? 'Login' : 'Sign Up'}</button>

        <button class="toggle-button" on:click={toggleMode}>
            {isLogin ? "Don't have an account? Sign up" : 'Already have an account? Login'}
        </button>
    </div>
</div>
