<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import NavBar from '../lib/components/NavBar.svelte';
	import Footer from '../lib/components/Footer.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="flex min-h-screen flex-col font-sans antialiased">
	<NavBar />
	<main class="flex-1">
		{@render children()}
	</main>
	<Footer />
</div>
