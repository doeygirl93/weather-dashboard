<script lang="ts">
    import { motion, useTime, useSpring, useTransform, useScroll } from '@humanspeak/svelte-motion'
    
    let targetEl: HTMLElement;

    const time = useTime()
    const progress = useTransform(() => ($time % 4000) / 4000, [time])
    
    const { scrollYProgress } = useScroll()
    const scaleX = useSpring(scrollYProgress, {
        stiffness: 100,
        damping: 30,
        restDelta: 0.001
    });
    // as scrolll goes from 0 to 1 opacity goes from 
    const opacity = useTransform(scrollYProgress, [0, 0.2], [1, 0]);
    // as scrolll goes from 0 to 1 text moves from 0 to -200 xp
    const y = useTransform(scrollYProgress, [0, 1], [0, -500]);
    const cat_opacity = useTransform(scrollYProgress, [0, 0.5], [1, 0]);
    // as scrolll goes from 0 to 1 text moves from 0 to -200 xp
    const cat_y = useTransform(scrollYProgress, [0.3, 1], [0, -200]);

    
</script>

<div class="fixed top-0 left-0 right-0 h-2 bg-blue-500 origin-left z-50"
  style:transform="scaleX({$scaleX})">


</div>
<main class="lottie-anime flex flex-col items-center justify-center bg-black">
    <section class=" min-w-full min-h-screen bg-emerald-600 text-white p-6">
        <h1 class="text-7xl"> Welcome to Weather dashboard</h1>
        <motion.ul drag dragSnapToOrigin
        class="size-24 rounded-md bg-pink-400"
        animate={{ rotate: 360 }}
        transition={{duration: 1}}

        />
        <div class="mt-[clamp(9rem,12vw,15rem)] w-full h-full flex flex-col items-center">
            <h1 class="text-7xl"
            style:opacity={$opacity} style:transform="translateY({$y}px)"
            > 
                Hello World
            </h1>
        </div>
        <div>
        <img alt="pfp" src="tab_cat_icon.jpg" class="size-24 rounded-2xl"
        style:opacity={$cat_opacity} style:transform="translateY({$cat_y}px)">
        </div>
    </section>

    <!-- <section class=" h-[200vh] bg-slate-900 test-white p-20">
        

    </section>
    -->

    <section class="site-hero min-w-full min-h-screen bg-amber-900 text-white p-6 flex flex-col">
        <div class="text-center">
            <motion.button
            class="button-hero text-2xl bg-linear-to-r from-indigo-500 via-purple-500 to-pink-500 shadow-2xs shadow-pink-600 font-semibold rounded-3xl p-[.5em] m-[2em] cursor-pointer hover:shadow-2xl"
            initial={{ scale: 0, opacity: 0, y:100 }}
            whileInView={{ 
                scale: 1,
                opacity: 1,
                 y: 0,
                transition: 2 
                }}
            whileHover={{ scale: 1.2}}
            whileTap={{ scale: 0.8 }}
            >
            Click me
            </motion.button>
        </div>
        
    </section>

    <section class="min-w-full min-h-screen bg-cyan-700 text-white p-6">
    About
    </section>
</main>