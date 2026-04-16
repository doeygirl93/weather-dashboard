<script lang="ts">
    import { onMount } from 'svelte';
    import gsap from 'gsap';
    import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';


    let button;
    // turns on scroll feat 
    
    gsap.registerPlugin(ScrollTrigger)

    onMount(() => {
        // This means the code only runs when the site is rendered for the user
        console.log("The browser is ready and devleivered")
        
        gsap.fromTo(
            ".button-hero", 
            {x: 50, opacity: 0}, 
        { x: 0, opacity: 1,duration: 1.5, ease: "bounce.out" })

        button.addEventListener("mouseenter", () => {
        gsap.to(button, {scale: 1.1, boxShadow: "0 25px 50px -12px rgba(291, 39, 119, 0.5)", duration: 0.3 });
        
        });
        button.addEventListener("mouseleave", () => {
        gsap.to(button, { scale: 1, boxShadow: "0 1px 2px 0 rgba(0, 0, 0, 0.05)", duration: 0.3 });
    });
        
    });

</script>


<main class="lottie-anime min-h-screen flex flex-col items-center justify-center bg-black">
    <section class=" min-w-full min-h-auto bg-emerald-600 text-white p-6">
        <h1 class="text-7xl"> Welcome to Weather dashboard</h1>
    </section>

    <section class="site-hero min-w-full min-h-auto bg-amber-900 text-white p-6 flex flex-col">
        <div class="text-center">
            <button bind:this={button} class="button-hero text-2xl bg-linear-to-r from-indigo-500 via-purple-500 to-pink-500 shadow-2xs shadow-pink-600 font-semibold rounded-3xl p-[.5em] m-[2em] cursor-pointer ease-in-out hover:scale-110 hover:shadow-2xl">
                Click me
            </button>
        </div>
    </section>

    <section class="min-w-full min-h-auto bg-cyan-700 text-white p-6">
    About
    </section>
</main>