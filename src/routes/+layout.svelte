<script lang="ts">
	import './layout.css';

	let { children } = $props();
</script>

<div class="app">

	<main>
		
	<nav>
		<a href="#site-start" class="absolute top-[-5] text-2xl text-black"> The start</a>
	</nav>
	{@render children()}
	</main>

	
</div>