<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import NavBar from '../lib/components/NavBar.svelte';
	import Footer from '../lib/components/Footer.svelte';

	import CursorSpotlight from '$lib/components/CursorSpotlight.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div
	class="flex min-h-screen flex-col bg-background-light font-sans text-gray-900 antialiased dark:bg-background-dark dark:text-gray-100"
>
	<CursorSpotlight />
	<NavBar />
	<main class="z-10 flex flex-1 flex-col">
		{@render children()}
	</main>
	<Footer />
</div>
