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
    const y1 = useTransform(scrollYProgress, [0, 1], [0, -350]);
    const y1_1 = useTransform(scrollYProgress, [0, 1], [0, -130]);
    const y2 = useTransform(scrollYProgress, [0, 1], [0, -225]);
    const y3 = useTransform(scrollYProgress, [0, 1], [0, 20]);

</script>



<!-- Progress Bar-->
<div class="fixed top-0 left-0 right-0 h-2 bg-blue-500 origin-left z-50"
  style:transform="scaleX({$scaleX})">
</div>



<main class="relative flex flex-col items-center justify-center bg-black overflow-hidden">
     <a href="/about"
     class="">
        <button 
            class="absolute z-100 top-0 right-0 mx-4 my-2 flex items-center gap-2 bg-black/20 hover:bg-slate-950/40 border-4 border-white/15 hover:border-emerald-white/50 backdrop-blur-md  px-4 py-2 rounded-4xl transition-all active:scale-95 hover:scale-110"
        >
            <span class="text-white/40 group-hover:text-white font-mono text-xs uppercase tracking-tighter">
                About Section
            </span>

        </button>
    </a>
    
    <section id="site-start" class="min-w-full min-h-[90dvh] bg-[linear-gradient(to_bottom,rgba(0,0,0,0.05)_0%,rgba(0,0,0,0)_80%,#031523_100%),url('/spacex-VBNb52J8Trk-unsplash.jpg')] bg-cover bg-center"
    style:transform="translateY({$y3}px)">


        <div class="relative mt-[clamp(5rem,10vw,18rem)] w-full h-full flex flex-col items-center text-center">
            
            <h1 class="will-change-transform text-7xl font-semibold tracking-tighter bg-linear-to-b from-blue-800 to-blue-950 bg-clip-text text-transparent"
            style:transform="translateY({$y1}px)"
            > 
            Welcome To The 
            <span 
            class="text-blue-950 tracking-wide absolute left-1/2 -translate-x-1/2 top-[60%] whitespace-nowrap"
            style:transform="translateY({$y1_1}px)"
            >
                Wheather Dashboard
            </span>
            </h1>

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
        class="size-42 rounded-md bg-[url('/rocket.png')] bg-cover bg-center"
        animate={{  scale: 1, opacity: 1, x: 0, y: [0, -200, 0], rotate: 360  }}
        transition={{
            rotate: {duration: 50, repeat: Infinity, ease: "linear"},
            y: { duration: 40, repeat: Infinity, repeatType: "reverse", ease: "easeInOut" }
        }} />
        </div>
        <div class="flex justify-start w-full">
            <motion.ul drag
            class="size-42 rounded-md bg-[url('/handsome_orphues.png')] bg-cover bg-center flex justify-end"
            animate={{  scale: 1, opacity: 1, x: 0, y: [0, -10, 0], rotate: 30  }}
            transition={{
            rotate: {duration: 3, repeat: Infinity, ease: "linear"},
            y: { duration: 10, repeat: Infinity, repeatType: "reverse", ease: "easeInOut" }
            }}
             />

        </div>
        <div class="flex flex-col items-center w-full">
            <motion.ul drag
            class="size-42 rounded-md bg-[url('/planet.png')] bg-cover bg-center flex justify-end"
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


    <section class=" min-w-full min-h-[190dvh] bg-[linear-gradient(to_top,rgba(0,0,0,0.05)_0%,rgba(0,0,.2,.5)_80%,#031523_100%),url('/ocean.jpg')] text-white p-6 flex flex-col">
        
        <div class="grid grid-cols-3 gap-20">
            <motion.div 
                class="col-span-2 border-4 border-white/10 bg-white/2.5 backdrop-blur-sm hover:backdrop-blur-md backdrop-saturate-150 rounded-2xl shadow-xl min-h-40 my-10"
                initial={{ opacity: 0, x:-100 }}
                whileInView={{ 
                    opacity: 1,
                    x: 0,
                    }}
                viewport={{ once: true }}
                animate={{ scale: 1 }} 
                whileHover={{ 
                    scale: 0.8,
                    transition: { duration: 0.3 } }}
                    
                whileTap={{scale: 1.125,}}
                transition={{
                    duration: .2,
                    scale: { type: "spring", stiffness: 400, damping: 10 },
                    default: { duration: 1 } 
                    }}
                >
                <div class="flex flex-col items-center w-full h-auto text-pink-50 p-4 md:p-8">
                    <h2 class="text-2xl">Feature [01] Photo Of the Day</h2>
                    <p class="text-md">Using the Nasa API we get the photo of the day to display the 
                        <span class="italic">beutful</span> 
                        photo that is chosen!
                    </p>
                </div>

            </motion.div>

            <div></div>
            <div></div>
            <motion.div 
            class="col-span-2 border-4  border-white/10 bg-white/2.5 backdrop-blur-sm hover:backdrop-blur-md backdrop-saturate-150  rounded-2xl shadow-xl  min-h-40 mb-10"
            initial={{ opacity: 0, x:100 }}
            whileInView={{ 
                opacity: 1,
                 x: 0,
                }}
            viewport={{ once: true }}
            animate={{ scale: 1 }} 
            whileHover={{ 
                scale: 0.8,
                transition: { duration: 0.3 } }}
                
            whileTap={{scale: 1.125,}}
            transition={{
                delay: 5,
                duration: .3,
                scale: { type: "spring", stiffness: 400, damping: 10 },
                default: { duration: 1 } 
                }}
                >

                <div class="flex flex-col items-center w-full h-auto text-pink-50 p-4 md:p-8">
                    <h2 class="text-2xl">Feature [02] Display of Time</h2>
                    <p class="text-md"> If your a Bum who can't bother to check ur clock for the time we also display veryv eryyyy accurately what the time is!
                    </p>
                </div>

            </motion.div>
            <motion.div
                class="col-span-2 border-4 border-white/10 bg-white/2.5 backdrop-blur-sm hover:backdrop-blur-md backdrop-saturate-150  rounded-2xl shadow-xl  min-h-40 my-10"
                initial={{ opacity: 0, x:-100 }}
                whileInView={{ 
                    opacity: 1,
                    x: 0,
                    }}
                viewport={{ once: true }}
                animate={{ scale: 1 }} 
                whileHover={{ 
                    scale: 0.8,
                    transition: { duration: 0.3 } }}
                    
                whileTap={{scale: 1.125,}}
                transition={{
                    duration: .2,
                    scale: { type: "spring", stiffness: 400, damping: 10 },
                    default: { duration: 1 } 
                    }}
                    >
                <div class="flex flex-col items-center w-full h-auto text-pink-50 p-4 md:p-8">
                    <h2 class="text-2xl">Feature [03] Local Wheather</h2>
                    <p class="text-md"> 
                        we feed your data and give it to claude code and we get to see where you local wheather is + we feed ur data to claude code for free credits🤭
                    </p>
                </div>   

            </motion.div>

            <div></div>
            <div></div>
            <motion.div 
                class="col-span-2 border-4 border-white/10 bg-white/2.5 backdrop-blur-sm hover:backdrop-blur-md backdrop-saturate-150  rounded-2xl shadow-xl  min-h-40 mb-10"
                initial={{ opacity: 0, x:-100 }}
                whileInView={{ 
                    opacity: 1,
                    x: 0,
                    }}
                viewport={{ once: true }}
                animate={{ scale: 1 }} 
                whileHover={{ 
                    scale: 0.8,
                    transition: { duration: 0.3 } }}
                    
                whileTap={{scale: 1.125,}}
                transition={{
                    duration: .2,
                    scale: { type: "spring", stiffness: 400, damping: 10 },
                    default: { duration: 1 } 
                    }}
                    >

                <div class="flex flex-col items-center w-full h-auto text-pink-50 p-4 md:p-8">
                    <h2 class="text-2xl">Credits</h2>
                    <p class="text-md"> 
                        This website was made by ur gurl chika
                    </p>
                </div> 
            </motion.div>

        </div>
        <!-- Button -->

        <div class="text-center">

        <a href="/dashboard">
         <motion.button
            class=" text-2xl bg-linear-to-r from-indigo-500 via-purple-500 to-pink-500 shadow-2xs shadow-pink-600 font-semibold rounded-3xl p-[.5em] m-[2em] cursor-pointer hover:shadow-2xl"
            href="/about"
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
            Click me to go to dashboard
            </motion.button>
        </a>
        </div>
        
    </section>

</main>