<script lang="ts">
	import * as m from '$lib/paraglide/messages';

	export let title: string;
	export let category: string;
	export let description: string;
	export let image: string | null = null;
	export let link: string = '#';
	export let alt: string = '';
</script>

<div
	class="group relative flex flex-col overflow-hidden rounded-2xl bg-gray-50 transition-all hover:-translate-y-1 hover:shadow-2xl dark:bg-surface-dark"
>
	<!-- Image / Placeholder -->
	<div class="relative aspect-video overflow-hidden bg-gray-200">
		{#if image}
			<img
				src={image}
				{alt}
				class="h-full w-full object-cover transition-transform duration-500 group-hover:scale-105"
			/>
		{:else}
			<div
				class="flex h-full w-full items-center justify-center bg-gradient-to-br from-gray-100 to-gray-200 dark:from-gray-700 dark:to-gray-800"
			>
				<span class="text-4xl">🚀</span>
			</div>
		{/if}

		<!-- Overlay -->
		<div
			class="absolute inset-0 bg-black/0 transition-colors duration-300 group-hover:bg-black/10"
		></div>
	</div>

	<!-- Content -->
	<div class="flex flex-1 flex-col p-6">
		<div class="mb-4">
			<span
				class="inline-flex items-center rounded-full bg-primary/10 px-3 py-1 text-xs font-medium text-primary ring-1 ring-primary/20 ring-inset"
			>
				{category}
			</span>
		</div>
		<h3 class="text-xl leading-6 font-semibold text-gray-900 dark:text-white">
			<a href={link} class="focus:outline-none">
				<span class="absolute inset-0" aria-hidden="true"></span>
				{title}
			</a>
		</h3>
		<p class="mt-4 flex-1 text-sm leading-6 text-gray-600 dark:text-gray-400">
			{description}
		</p>
		<div class="mt-6 flex items-center gap-x-2 text-primary">
			<span class="text-sm font-semibold">{m['portfolio_page.cta']()}</span>
			<svg
				class="h-4 w-4 transition-transform group-hover:translate-x-1"
				fill="none"
				viewBox="0 0 24 24"
				stroke="currentColor"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M17 8l4 4m0 0l-4 4m4-4H3"
				/>
			</svg>
		</div>
	</div>
</div>
