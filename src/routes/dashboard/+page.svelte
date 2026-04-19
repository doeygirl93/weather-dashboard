<script lang="ts">
    import { motion} from '@humanspeak/svelte-motion'

    import { onMount } from 'svelte';
    import { fade, blur } from 'svelte/transition';

    let userName = $state("");
    let isAuth = $state(false);


    // runs when the user first wants acess
    function auth() {
        if (userName.trim() !== "") {
            // saves to broswers long term mem
            localStorage.setItem("user_id", userName);
            // this stsate is what comfirms when we swithc the ui
            isAuth = true;
        }
    }

    // supposed to get the user's name if they have saved it
    onMount (() => {
        // ts runs once the page loads imeadately
        const savedName = localStorage.getItem("user_id");
        if (savedName) {
            userName = savedName;
            isAuth = true;
        }
    });
</script>

<svelte:head>
	<title>Dashboard</title>
	<meta name="description" content="About this app" />
</svelte:head>

{#if isAuth }
    <main class="h-screen w-full bg-[url('forest_cam.jpg')] bg-cover bg-center backdrop-blur-xl flex flex-col items-center justify-center p-4">
        <div transition:blur={{ duration: 800}} class="">
            <div class="flex flex-col item-center size-95 bg-amber-50 rounded-3xl">


            </div>
            <!--
            <h1> Whats ur Name CHild </h1>
            <input bind:value={userName}/>
            <button onclick={auth}> ACESS DASHBOARD</button>
-->
        </div>



    </main>
{:else}
    <div in:fade={{ delay: 400}} class="p-20 text-white font-mono bg-red-400">
        <h1> {userName}, welcome back to the Dashboard</h1>
        <p> Lorem ipsum dolor sit amet consectetur adipisicing elit. Quos reprehenderit ut consectetur sint commodi suscipit officia expedita culpa rerum et eius obcaecati quaerat qui, ad, accusamus temporibus possimus? Explicabo, sint!</p>


    </div>
{/if}