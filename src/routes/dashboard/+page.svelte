<script lang="ts">
    import { PUBLIC_NASA_API_KEY } from '$env/static/public';
    import { motion} from '@humanspeak/svelte-motion'

    import { onMount } from 'svelte';
    import { fade, blur } from 'svelte/transition';

    let userName = $state("");
    let isAuth = $state(false);

    let time = $state(new Date());

    let timeString = $derived(time.toLocaleTimeString());

    let backgroundImage = $state("")

    let lat = $state(0);
    let lon = $state(0);
    let weather = $state({ temp: "--", description: "Loading Data . . . "});

    let quote = $state({text: "Loading sora AI + Chatgpt . ..  . . . ", author: "Ur gurl"});

    async function getNasaPhoto() {
        try {
            const response = await fetch(`https://api.nasa.gov/planetary/apod?api_key=${PUBLIC_NASA_API_KEY}`);

            if (!response.ok) throw new Error("NASA API connection failed");

            const data = await response.json();

            backgroundImage = data.url;
        } catch (error) {
            console.error("Cosmic Error:", error);
            backgroundImage = "bc_bg_img.jpg"
        }
    }

    async function getWeather() {
        // gets cords from browser
        navigator.geolocation.getCurrentPosition(async (position) => {
            lat = position.coords.latitude;
            lon = position.coords.longitude;

            try {
                // get weather basrd on the corsd
                
                const res = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current=temperature_2m,relative_humidity_2m,weather_code&temperature_unit=fahrenheit`)
                const data = await res.json();

                weather = {
                    temp: Math.round(data.current.temperature_2m),
                    description: "Conditions: "
                };
            } catch (e) {
                console.error("Weather API failed", e);
           }
        }); 
    }

        async function getQuotes() {
            try{
            const res = await fetch('https://corsproxy.io/?https://zenquotes.io/api/random')
            const data = await res.json();

            quote = {
                text: data[0].q,
                author: data[0].a
            };

        } catch (e) {
            quote = { text: "You must be Git, because I can’t commit without you ", author: "r/ProgrammerHumor" };
        }
    };


    // runs when the user first wants acess
    function auth() {
        if (userName.trim() !== "") {
            // saves to broswers long term mem
            localStorage.setItem("user_id", userName);
            // this stsate is what comfirms when we swithc the ui
            isAuth = true;
        }
    };

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

        getNasaPhoto();

        getWeather();

        getQuotes();

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
    <main
    class="h-screen w-full bg-cover bg-cover transition-all duration-1000 flex items-center justify-center relative overflow-hidden"
    style="background-image:url('{backgroundImage}')"
    >

        <div class="absolute inset-0 bg-black/40 backdrop-blur-[2px]"></div>

        <section class="relative z-10 text-center">
            <div class="clock-box bg-white/10 backdrop-blur-xl p-10 rounded-3xl border border-white/20">
                <h2 class="text-green-400 font-mono tracking-widest test-sm mb-2 uppercase">Welcome Back {userName}</h2>
                <p class="text-8xl font-mono text-white font-bold drop-shadow-2xl">{timeString}</p>
                <div class="flex justify-around items-center font-mono">
                    <div class="text-left">
                        <p> External Temo </p>
                        <p> {weather.temp} C</p>
                    </div>
                    <!--
                    <div class="text-right">
                        <p> Weather Desc </p>
                        <p> {weather.description} C</p>
                    </div>
                    -->

                </div>

            </div>

        
            <div in:fade={{ delay: 400}} class="">
            <p class="text-shadow-[-1px_-1px_0_#000,1px_-1px_0_#000,-1px_1px_0_#000,1px_1px_0_#000] text-white italic"> Welcome back {userName}</p>


            </div>

            <footer class="absolute bottom-[-60] left-0 w-full flex flex-col items-center px-4">
                <div class="w-2xl text-center cursor-pointer" >
                    <p class="text-white/80 font-mono italic text-lg drop-shadow-md transition-all hover:text-white">
                        "{quote.text}"
                    </p>
                    <p class="text-white/80 font-mono italic text-lg drop-shadow-md transition-all hover:text-white">
                        "{quote.author}"
                    </p>

                    <button onclick={getQuotes}>
                        <span class="text-green-400/80 font-mono italic text-lg drop-shadow-md transition-all hover:scale-110 hover:text-green-400">
                            Click For Further enlightenment
                        </span>
                    </button>
                </div>
            
            </footer>
        </section>

    </main>
{/if}