<script lang="ts">
    import { motion, useTime, useSpring, useTransform, useScroll } from '@humanspeak/svelte-motion'
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
    const y1 = useTransform(scrollYProgress, [0, 1], [0, -100]);
    const y2 = useTransform(scrollYProgress, [0, 1], [0, -125]);
    const y3 = useTransform(scrollYProgress, [0, 1], [0, 20]);

</script>



<!-- Progress Bar-->
<div class="fixed top-0 left-0 right-0 h-2 bg-blue-500 origin-left z-50"
  style:transform="scaleX({$scaleX})">
</div>



<main class="flex flex-col items-center justify-center bg-black">
    <section class="min-w-full min-h-[90dvh] bg-[linear-gradient(to_bottom,rgba(0,0,0,0.05)_0%,rgba(0,0,0,0)_80%,#031523_100%),url('spacex-VBNb52J8Trk-unsplash.jpg')] bg-cover bg-center"
    style:transform="translateY({$y3}px)">


        <div class="mt-[clamp(5rem,10vw,18rem)] w-full h-full flex flex-col items-center text-center">
            <h1 class="text-7xl font-semibold tracking-tighter bg-linear-to-b from-blue-800 to-blue-950 bg-clip-text text-transparent"
           style:transform="translateY({$y1}px)"
            > 
                Welcome To The Weather Dashboard
            </h1>
        </div>

        <p 
        class="m-10 text-center text-md tracking-wider text-shadow-lg text-shadow-black/30"
        style:transform="translateY({$y2}px)"
        >
        Made wit 🥶 by Queen Von
        </p>


        <!-- Stickers-->
         <div class="flex justify-end w-full">
        <motion.ul drag
        class="size-42 rounded-md bg-[url('rocket.png')] bg-cover bg-center"
        animate={{ rotate: 360 }}
        transition={{duration: 1}} />
        </div>
        <div class="flex justify-start w-full">
            <motion.ul drag
            class="size-42 rounded-md bg-[url('handsome_orphues.png')] bg-cover bg-center flex justify-end"
            animate={{ rotate: 360 }}
            transition={{duration: 1}} />
        </div>
        <div class="flex flex-col items-center w-full">
            <motion.ul drag
            class="size-42 rounded-md bg-[url('planet.png')] bg-cover bg-center flex justify-end"
            initial={{ scale: 0, opacity: 0, x:101 }}
            animate={{  scale: 1, opacity: 1, x: 0  }}
            transition={{duration: 1}} />
        </div>
    </section>

    <!-- <section class=" h-[200vh] bg-slate-900 test-white p-20">
        

    </section>
    -->


    <section class="site-hero min-w-full min-h-[190dvh] bg-[#031523] text-white p-6 flex flex-col">
        
        
        <!-- Button -->
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

</main>