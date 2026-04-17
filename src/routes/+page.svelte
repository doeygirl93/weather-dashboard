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
            <motion.h1 class="will-change-transform text-7xl font-semibold tracking-tighter bg-linear-to-b from-blue-800 to-blue-950 bg-clip-text text-transparent"
           style={{ translateY: y1 }}
            > 
                Welcome To The Weather Dashboard
            </motion.h1>
        </div>

        <p 
        class="will-change-transform m-10 text-center text-md tracking-wider text-shadow-lg text-shadow-black/30"
        style:transform="translateY({$y2}px)"
        >
        Made wit 🥶 by Queen Von
        </p>


        <!-- Stickers-->
         <div class="flex justify-end w-full">
        <motion.ul drag
        class="size-42 rounded-md bg-[url('rocket.png')] bg-cover bg-center"
        animate={{  scale: 1, opacity: 1, x: 0, y: [0, -200, 0], rotate: 360  }}
        transition={{
            rotate: {duration: 50, repeat: Infinity, ease: "linear"},
            y: { duration: 40, repeat: Infinity, repeatType: "reverse", ease: "easeInOut" }
        }} />
        </div>
        <div class="flex justify-start w-full">
            <motion.ul drag
            class="size-42 rounded-md bg-[url('handsome_orphues.png')] bg-cover bg-center flex justify-end"
            animate={{  scale: 1, opacity: 1, x: 0, y: [0, -10, 0], rotate: 30  }}
            transition={{
            rotate: {duration: 3, repeat: Infinity, ease: "linear"},
            y: { duration: 10, repeat: Infinity, repeatType: "reverse", ease: "easeInOut" }
            }}
             />

        </div>
        <div class="flex flex-col items-center w-full">
            <motion.ul drag
            class="size-42 rounded-md bg-[url('planet.png')] bg-cover bg-center flex justify-end"
            initial={{ scale: 0, opacity: 0, x:101 }}
            animate={{  scale: 1, opacity: 1, x: 0, y: [0, 15, 0], rotate: 360  }}
            transition={{
                rotate: {duration: 20, repeat: Infinity, ease: "linear"},
                y: { duration: 2, repeat: Infinity, repeatType: "reverse", ease: "easeInOut" }
            }}/>
        </div>
    </section>

    <!-- <section class=" h-[200vh] bg-slate-900 test-white p-20">
        

    </section>
    -->


    <section class=" min-w-full min-h-[190dvh] bg-[#031523] text-white p-6 flex flex-col">
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-10">




        </div>
        <!-- Button -->

        <div class="text-center">
         <motion.button
            class=" text-2xl bg-linear-to-r from-indigo-500 via-purple-500 to-pink-500 shadow-2xs shadow-pink-600 font-semibold rounded-3xl p-[.5em] m-[2em] cursor-pointer hover:shadow-2xl"
            initial={{ scale: 0, opacity: 0, y:100 }}
            whileInView={{ 
                scale: 1,
                opacity: 1,
                 y: 0,
                }}
            viewport={{ once: true }}

            /* define animate so it can be like the bases pos*/

            animate={{ scale: 1 }} 
            whileHover={{ 
                scale: 1.2,
                transition: { duration: 0.3 } }}
                
            whileTap={{scale: 0.8,}}
            transition={{
                duration: .2,
                scale: { type: "spring", stiffness: 400, damping: 10 },
                default: { duration: 1 } 
                }}
            >
            Click me
            </motion.button>
        </div>
        
    </section>

</main>