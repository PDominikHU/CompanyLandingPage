<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { slide } from 'svelte/transition';

	let openIndex = $state<number | null>(0);

	function toggle(index: number) {
		openIndex = openIndex === index ? null : index;
	}

	const faqs = [
		{ q: () => m['faq.q1'](), a: () => m['faq.a1']() },
		{ q: () => m['faq.q2'](), a: () => m['faq.a2']() },
		{ q: () => m['faq.q3'](), a: () => m['faq.a3']() },
		{ q: () => m['faq.q4'](), a: () => m['faq.a4']() },
		{ q: () => m['faq.q5'](), a: () => m['faq.a5']() }
	];
</script>

<section
	class="border-t border-gray-100 bg-white py-24 transition-colors dark:border-gray-800 dark:bg-surface-dark"
>
	<div class="mx-auto max-w-4xl px-4 sm:px-6 lg:px-8">
		<div class="mb-16 text-center">
			<h2 class="text-3xl font-black text-gray-900 md:text-5xl dark:text-white">
				{m['faq.title']()}
			</h2>
			<p class="mx-auto mt-4 max-w-2xl text-lg text-gray-500 dark:text-gray-400">
				{m['faq.subtitle']()}
			</p>
		</div>

		<div class="space-y-4">
			{#each faqs as faq, i}
				<div
					class="overflow-hidden rounded-2xl border border-gray-100 bg-background-light transition-all dark:border-gray-700 dark:bg-background-dark {openIndex ===
					i
						? 'ring-2 ring-primary/20 dark:ring-primary/40'
						: ''}"
				>
					<button
						class="flex w-full items-center justify-between px-6 py-5 text-left transition-colors hover:bg-gray-50 dark:hover:bg-gray-800"
						onclick={() => toggle(i)}
					>
						<span
							class="text-lg font-bold text-gray-900 dark:text-white {openIndex === i
								? 'dark:text-primary-400 text-primary'
								: ''}"
						>
							{faq.q()}
						</span>
						<span
							class="ml-6 flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-white text-xl text-primary shadow-sm transition-transform duration-300 dark:bg-gray-700 dark:text-white {openIndex ===
							i
								? 'rotate-180 bg-primary text-white dark:bg-primary'
								: ''}"
						>
							{openIndex === i ? '−' : '+'}
						</span>
					</button>
					{#if openIndex === i}
						<div transition:slide={{ duration: 300, axis: 'y' }}>
							<div
								class="border-t border-gray-100 px-6 py-5 text-gray-600 dark:border-gray-700 dark:text-gray-300"
							>
								{faq.a()}
							</div>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</section>
