<script lang="ts">
    import { onMount } from 'svelte';
    import gsap from 'gsap';
    import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';



    // turns on scroll feat 

    gsap.registerPlugin(ScrollTrigger)

    onMount(() => {
        // This means the code only runs when the site is rendered for the user
        console.log("The browser is ready and devleivered")
        gsap.to(
            ".button-hero", 
            { x: 200, delay: 1, duration: 1.5, ease: "bounce"});


        
    });

</script>
<main class="lottie-anime min-h-screen flex flex-col items-center justify-center bg-black">
    <section class=" min-w-full min-h-auto bg-emerald-600 text-white p-6">
        <h1 class="text-7xl"> Welcome to Weather dashboard</h1>
    </section>

    <section class="site-hero min-w-full min-h-auto bg-amber-900 text-white p-6 flex flex-col">
        <div class="">
            <button class="button-hero text-2xl bg-linear-to-r from-indigo-500 via-purple-500 to-pink-500 shadow-2xs shadow-pink-600 font-semibold rounded-3xl p-[.5em] m-[2em] cursor-pointer transition-all duration-300 ease-in-out hover:scale-110 hover:shadow-2xl">
                Click me
            </button>
        </div>
    </section>

    <section class="something-tocome min-w-full min-h-auto bg-cyan-700 text-white p-6">
    About
    </section>
</main>