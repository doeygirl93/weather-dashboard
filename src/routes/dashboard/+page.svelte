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

<svelte:head>
	<title>Dashboard</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div>
	<h1 class="text-7xl text-center">TS the dashboard </h1>

	<p>
		This made by chika finna be done sooon
	</p>
</div>

        <a href="/">
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
            Click me to go BACK
            </motion.button>
        </a>
