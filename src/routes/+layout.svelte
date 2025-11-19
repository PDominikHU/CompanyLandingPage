<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import NavBar from '../components/NavBar.svelte';
	import Footer from '../components/Footer.svelte';

	let { children } = $props();
</script>

<NavBar/>
<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children()}

<Footer/>