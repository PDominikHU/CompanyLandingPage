<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { fade, slide } from 'svelte/transition';
	import { onMount } from 'svelte';

	let visible = $state(false);

	onMount(() => {
		const observer = new IntersectionObserver(
			(entries) => {
				if (entries[0].isIntersecting) {
					visible = true;
					observer.disconnect();
				}
			},
			{ threshold: 0.1 }
		);

		const el = document.getElementById('stats-section');
		if (el) observer.observe(el);

		return () => observer.disconnect();
	});

	// Animated counter
	function count(node: HTMLElement, { from = 0, to = 100, duration = 2000 }) {
		return {
			duration,
			tick: (t: number) => {
				const val = Math.round(from + (to - from) * t);
				node.textContent = val.toString();
			}
		};
	}
</script>

<section
	id="stats-section"
	class="relative overflow-hidden border-y border-gray-100 bg-white py-16 text-primary dark:border-gray-800 dark:bg-background-dark dark:text-gray-100"
>
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
		{#if visible}
			<div class="grid grid-cols-2 gap-8 md:grid-cols-4">
				<div class="text-center" in:fade={{ delay: 0, duration: 800 }}>
					<p class="text-4xl font-black md:text-5xl">
						<span in:count={{ to: 50, duration: 2000 }}>0</span>+
					</p>
					<p
						class="mt-2 text-sm font-semibold tracking-wider text-gray-500 uppercase dark:text-gray-400"
					>
						{m['stats.projects']()}
					</p>
				</div>
				<div class="text-center" in:fade={{ delay: 200, duration: 800 }}>
					<p class="text-4xl font-black md:text-5xl">
						<span in:count={{ to: 5, duration: 2000 }}>0</span>+
					</p>
					<p
						class="mt-2 text-sm font-semibold tracking-wider text-gray-500 uppercase dark:text-gray-400"
					>
						{m['stats.experience']()}
					</p>
				</div>
				<div class="text-center" in:fade={{ delay: 400, duration: 800 }}>
					<p class="text-4xl font-black md:text-5xl">
						<span in:count={{ to: 100, duration: 2000 }}>0</span>%
					</p>
					<p
						class="mt-2 text-sm font-semibold tracking-wider text-gray-500 uppercase dark:text-gray-400"
					>
						{m['stats.clients']()}
					</p>
				</div>
				<div class="text-center" in:fade={{ delay: 600, duration: 800 }}>
					<p class="text-4xl font-black md:text-5xl">
						<span in:count={{ to: 6, duration: 2000 }}>0</span>
					</p>
					<p
						class="mt-2 text-sm font-semibold tracking-wider text-gray-500 uppercase dark:text-gray-400"
					>
						{m['stats.support']()}
					</p>
				</div>
			</div>
		{/if}
	</div>
</section>
