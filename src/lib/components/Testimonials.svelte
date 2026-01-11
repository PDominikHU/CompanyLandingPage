<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { fade } from 'svelte/transition';

	// Helper to get localized quotes
	const getReviews = () => [
		{
			text: m['testimonials.review1_text'](),
			name: m['testimonials.review1_name'](),
			role: m['testimonials.review1_role']()
		},
		{
			text: m['testimonials.review2_text'](),
			name: m['testimonials.review2_name'](),
			role: m['testimonials.review2_role']()
		},
		{
			text: m['testimonials.review3_text'](),
			name: m['testimonials.review3_name'](),
			role: m['testimonials.review3_role']()
		}
	];
</script>

<section
	class="bg-background-light py-20 text-gray-900 transition-colors dark:bg-background-dark dark:text-gray-100"
>
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
		<div class="mb-16 text-center">
			<h2 class="text-3xl font-black md:text-5xl">{m['testimonials.title']()}</h2>
			<p class="mx-auto mt-4 max-w-2xl text-lg text-gray-500 dark:text-gray-400">
				{m['testimonials.subtitle']()}
			</p>
		</div>

		<div class="grid gap-8 md:grid-cols-3">
			{#each getReviews() as review, i}
				<div
					data-aos="fade-up"
					data-aos-delay={i * 100}
					class="relative rounded-2xl bg-white p-8 shadow-sm transition-transform hover:-translate-y-2 dark:bg-surface-dark"
				>
					<!-- Quote Icon -->
					<div class="absolute top-6 right-8 font-serif text-6xl text-primary/10">"</div>

					<p class="relative z-10 mb-6 text-lg leading-relaxed font-light italic">
						{review.text}
					</p>

					<div class="flex items-center gap-4">
						<div
							class="flex h-12 w-12 items-center justify-center rounded-full bg-primary/20 text-xl font-bold text-primary"
						>
							{review.name.charAt(0)}
						</div>
						<div>
							<h4 class="font-bold">{review.name}</h4>
							<p class="text-xs text-gray-500 uppercase dark:text-gray-400">{review.role}</p>
						</div>
					</div>
				</div>
			{/each}
		</div>
	</div>
</section>
