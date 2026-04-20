<script lang="ts">
    import { motion} from '@humanspeak/svelte-motion'

    import { onMount } from 'svelte';
    import { fade, blur } from 'svelte/transition';

    let userName = $state("");
    let isAuth = $state(false);

    let time = $state(new Date());

    let timeString = $derived(time.toLocaleTimeString());


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
        const interval = setInterval(() => {
            time= new Date()
        }, 1000);

        return () => clearInterval(interval);

        

    });
</script>

<svelte:head>
	<title>Dashboard</title>
	<meta name="description" content="About this app" />
</svelte:head>

{#if !isAuth }
    <main class="h-screen w-full bg-[url('forest_cam.jpg')] bg-cover bg-center backdrop-blur-xl flex flex-col items-center justify-center p-4">
        <div transition:blur={{ duration: 800}} class="">

            <!-- Ts the box-->
            <motion.div 
            class="flex flex-col item-center w-95 h-60 bg-amber-50 rounded-3xl border-2 border-green-950"
            initial={{ scale: 0.8, opacity: 0, x:-100 }}
            animate={{
                scale: 1,
                opacity: 1,
                 x: 0}}
            transition={{duration: .8}}
                 >

                <div class="w-full h-full grid grid-rows-4">
                    <div class=" flex flex-col items-center p-5 bg-green-800 rounded-t-3xl">
                        <h1 class="text-4xl text-white/90 font-extrabold font-mono"> Dashboard Portal </h1>
                    </div>
                    <div class="flex flex-col items-center">
                        <p class="text-sm italic text-black/70"> Enter your Name to login in to the dashboard</p>
                    </div>
                    <div class=" flex flex-row items-center p-2 pb-16">
                        <img src="tab_cat_icon.jpg" alt="cat icon" class="size-12 rounded-full mr-10"/>
                        <input bind:value={userName} class="border border-slate-100 rounded-4xl"/>
                    </div>

                    <div class=" flex flex-col items-center">
                        <motion.button 
                            onclick={auth}
                            class="h-10 text-center bg-red-700 text-xl font-extrabold border-2 border-black rounded-2xl px-6 text-white/90 shadow-lg hover:shadow-red-500/50"
                            animate={{ scale: 1 }} 
                            whileHover={{ 
                                scale: 1.1,
                                transition: { duration: 0.3 } }}
                                
                            whileTap={{scale: 0.9,}}
                            transition={{
                                duration: .2,
                                scale: { type: "spring", stiffness: 400, damping: 10 },
                                default: { duration: 1 } 
                                }}
                        >
                        CONFIRM
                        </motion.button>
                    </div>
                </div>
            </motion.div>
        </div>
        
    </main>
{:else}
    <section>
        <div class="clock-box">
            <p class="text-6xl font-mono ">{timeString}</p>
        </div>
    
        <div in:fade={{ delay: 400}} class="">


        </div>
    </section>
{/if}