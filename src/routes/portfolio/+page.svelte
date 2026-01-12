<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';
	import ProjectCard from '$lib/components/ProjectCard.svelte';

	let mounted = false;

	onMount(() => {
		mounted = true;
	});
</script>

<svelte:head>
	<title>{m['portfolio_page.title']()} | Company</title>
	<meta name="description" content={m['portfolio_page.subtitle']()} />
</svelte:head>

<div class="min-h-screen bg-white pb-20 dark:bg-background-dark">
	<!-- Hero Section -->
	<section class="relative overflow-hidden pt-32 pb-16 md:pt-48 md:pb-32">
		<div class="absolute inset-x-0 top-0 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80">
			<div
				class="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-primary to-[#9089fc] opacity-20 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]"
				style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
			></div>
		</div>

		<div class="mx-auto max-w-7xl px-6 lg:px-8">
			<div class="mx-auto max-w-2xl text-center">
				{#if mounted}
					<h1
						in:fly={{ y: 20, duration: 800 }}
						class="text-4xl font-bold tracking-tight text-gray-900 sm:text-6xl dark:text-white"
					>
						{m['portfolio_page.title']()}
					</h1>
					<p
						in:fly={{ y: 20, duration: 800, delay: 200 }}
						class="mt-6 text-lg leading-8 text-gray-600 dark:text-gray-300"
					>
						{m['portfolio_page.subtitle']()}
					</p>
				{/if}
			</div>
		</div>
	</section>

	<!-- Projects Grid -->
	<section class="mx-auto max-w-7xl px-6 lg:px-8">
		<div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
			{#if mounted}
				<div in:fly={{ y: 50, duration: 800, delay: 400 }} class="h-full">
					<ProjectCard
						title={m['demo_project.title']()}
						category={m['demo_project.category']()}
						description={m['demo_project.description']()}
						image={null}
						link="#"
						alt={m['demo_project.alt']()}
					/>
				</div>
				<div in:fly={{ y: 50, duration: 800, delay: 500 }} class="h-full">
					<ProjectCard
						title={m['portfolio_page.project1.title']()}
						category={m['portfolio_page.project1.category']()}
						description={m['portfolio_page.project1.description']()}
						image={null}
						link="#"
						alt={m['portfolio_page.project1.alt']()}
					/>
				</div>
				<div in:fly={{ y: 50, duration: 800, delay: 600 }} class="h-full">
					<ProjectCard
						title={m['portfolio_page.project2.title']()}
						category={m['portfolio_page.project2.category']()}
						description={m['portfolio_page.project2.description']()}
						image={null}
						link="#"
						alt={m['portfolio_page.project2.alt']()}
					/>
				</div>
			{/if}
		</div>
	</section>
</div>
