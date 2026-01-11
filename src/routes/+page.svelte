<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade } from 'svelte/transition';
	import * as m from '$lib/paraglide/messages';
	import CardComponent from '$lib/components/ValuesCard.svelte';
	import TeamCard from '$lib/components/TeamCard.svelte';
	import WhyUsCard from '$lib/components/WhyUsCard.svelte';
	import Testimonials from '$lib/components/Testimonials.svelte';
	import FAQ from '$lib/components/FAQ.svelte';

	let mounted = $state(false);

	function typewriter(node: HTMLElement, { speed = 1 }) {
		const text = node.textContent ?? '';
		const duration = text.length / (speed * 0.015);
		return {
			duration,
			tick: (t: number) => {
				const i = Math.trunc(text.length * t);
				node.textContent = text.slice(0, i);
			}
		};
	}

	let visibleSections = $state({
		mission: false,
		values: false,
		team: false,
		whyus: false
	});

	onMount(() => {
		mounted = true;

		const observer = new IntersectionObserver(
			(entries) => {
				entries.forEach((entry) => {
					if (entry.isIntersecting) {
						const section = entry.target.getAttribute('data-section');
						if (section) visibleSections[section as keyof typeof visibleSections] = true;
					}
				});
			},
			{ threshold: 0.1 }
		);

		document.querySelectorAll('section[data-section]').forEach((s) => observer.observe(s));
		return () => observer.disconnect();
	});
</script>

<svelte:head>
	<title>{m.home_title()}</title>
	<meta name="description" content={m.home_meta_desc()} />
</svelte:head>

<section class="relative overflow-hidden">
	<div class="absolute inset-0 bg-background-light dark:bg-background-dark"></div>
	<div class="relative mx-auto max-w-6xl px-4 py-20 sm:px-6 md:py-32 lg:px-8">
		<div class="flex min-h-[480px] flex-col items-center justify-center gap-6 text-center">
			{#if mounted}
				<h1
					in:typewriter={{ speed: 2.5 }}
					class="text-4xl leading-tight font-black tracking-wide text-gray-900 sm:text-5xl md:text-6xl dark:text-white"
				>
					{m['hero.title']()}
				</h1>
				<h2
					in:fade={{ delay: 800, duration: 1000 }}
					class="max-w-3xl text-base leading-normal font-normal text-gray-600 sm:text-lg dark:text-gray-300"
				>
					{m['hero.subtitle']()}
				</h2>
				<div in:fade={{ delay: 1000 }} class="mt-4 flex flex-wrap justify-center gap-4">
					<button
						onclick={() => (window.location.href = '/contact')}
						class="animate-glow flex h-12 min-w-40 cursor-pointer items-center justify-center rounded-lg bg-primary px-5 text-base font-bold text-white transition-all hover:scale-105 hover:bg-primary/90"
					>
						{m['navbar.lang']()}
					</button>
					<button
						onclick={() => (window.location.href = '/services')}
						class="flex h-12 min-w-40 cursor-pointer items-center justify-center rounded-lg bg-gray-200 px-5 text-base font-bold text-gray-800 transition-colors hover:bg-gray-300 dark:bg-gray-700 dark:text-white dark:hover:bg-gray-600"
					>
						{m.services()}
					</button>
				</div>
			{/if}
		</div>
	</div>
</section>

<section
	data-section="mission"
	class="border-t border-gray-100 bg-white py-16 md:py-24 dark:border-gray-800 dark:bg-surface-dark"
>
	<div class="relative mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
		{#if visibleSections.mission}
			<div in:fly={{ y: 50, duration: 800 }} class="grid items-start gap-8 md:grid-cols-12">
				<div class="md:col-span-4">
					<h2 class="text-3xl font-bold tracking-tight text-gray-900 md:text-4xl dark:text-white">
						{m['mission.title']()}
					</h2>
					<div class="mt-4 h-1 w-12 rounded bg-primary"></div>
				</div>
				<div class="md:col-span-8">
					<p class="text-lg leading-relaxed text-gray-600 dark:text-gray-300">
						{m['mission.text']()}
					</p>
				</div>
			</div>
		{/if}
	</div>
</section>

<section
	data-section="values"
	class="border-t border-gray-100 bg-background-light py-16 md:py-24 dark:border-gray-800 dark:bg-background-dark"
>
	<div class="mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
		<div class="mb-12 text-center">
			<h2 class="text-3xl leading-tight font-bold text-gray-900 dark:text-white">
				{m['values.title']()}
			</h2>
			<p class="mx-auto mt-4 max-w-2xl text-gray-600 dark:text-gray-300">
				{m['values.subtitle']()}
			</p>
		</div>
		{#if visibleSections.values}
			<div
				in:fly={{ y: 50, duration: 800, delay: 200 }}
				class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-5"
			>
				<CardComponent
					icon="🎖️"
					title={m['values.prof.title']()}
					description={m['values.prof.desc']()}
				/>
				<CardComponent
					icon="🛡️"
					title={m['values.trust.title']()}
					description={m['values.trust.desc']()}
				/>
				<CardComponent
					icon="👁️"
					title={m['values.transp.title']()}
					description={m['values.transp.desc']()}
				/>
				<CardComponent
					icon="👥"
					title={m['values.client.title']()}
					description={m['values.client.desc']()}
				/>
				<CardComponent
					icon="💡"
					title={m['values.innov.title']()}
					description={m['values.innov.desc']()}
				/>
			</div>
		{/if}
	</div>
</section>

<section
	data-section="team"
	class="border-t border-gray-100 bg-white py-16 md:py-24 dark:border-gray-800 dark:bg-surface-dark"
>
	<div class="mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
		<div class="mb-12 text-center">
			<h2 class="text-3xl leading-tight font-bold text-gray-900 dark:text-white">
				{m['team.title']()}
			</h2>
			<p class="mx-auto mt-4 max-w-2xl text-gray-600 dark:text-gray-300">{m['team.subtitle']()}</p>
		</div>
		{#if visibleSections.team}
			<div
				in:fly={{ y: 50, duration: 800, delay: 200 }}
				class="grid grid-cols-1 gap-8 sm:grid-cols-2 lg:grid-cols-3"
			>
				<TeamCard
					pic="/images/team/rock.jpg"
					name={m['team.members.member1.name']()}
					job={m['team.members.member1.job']()}
				/>
				<TeamCard
					pic="/images/team/rock.jpg"
					name={m['team.members.member2.name']()}
					job={m['team.members.member2.job']()}
				/>
				<TeamCard
					pic="/images/team/rock.jpg"
					name={m['team.members.member3.name']()}
					job={m['team.members.member3.job']()}
				/>
			</div>
		{/if}
	</div>
</section>

<Testimonials />

<section
	data-section="whyus"
	class="border-t border-gray-100 bg-background-light py-16 md:py-24 dark:border-gray-800 dark:bg-background-dark"
>
	<div class="mx-auto max-w-6xl px-4 sm:px-6 lg:px-8">
		<div class="mb-12 text-center">
			<h2 class="text-3xl leading-tight font-bold text-gray-900 dark:text-white">
				{m['whyus.title']()}
			</h2>
			<p class="mx-auto mt-4 max-w-2xl text-gray-600 dark:text-gray-300">{m['whyus.subtitle']()}</p>
		</div>
		{#if visibleSections.whyus}
			<div
				in:fly={{ y: 50, duration: 800, delay: 200 }}
				class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3"
			>
				<WhyUsCard title={m['whyus.card1_t']()} description={m['whyus.card1_d']()} />
				<WhyUsCard title={m['whyus.card2_t']()} description={m['whyus.card2_d']()} />
				<WhyUsCard title={m['whyus.card3_t']()} description={m['whyus.card3_d']()} />
				<WhyUsCard title={m['whyus.card4_t']()} description={m['whyus.card4_d']()} />
				<WhyUsCard title={m['whyus.card5_t']()} description={m['whyus.card5_d']()} />
				<WhyUsCard title={m['whyus.card6_t']()} description={m['whyus.card6_d']()} />
			</div>
		{/if}
	</div>
</section>

<FAQ />

<section class="relative overflow-hidden bg-primary py-24">
	<div
		class="absolute -top-24 -right-24 size-96 animate-pulse rounded-full bg-white/10 blur-3xl"
	></div>
	<div
		class="absolute -bottom-24 -left-24 size-96 animate-pulse rounded-full bg-black/10 blur-3xl"
		style="animation-delay: 2s;"
	></div>

	<div class="relative mx-auto max-w-4xl px-4 text-center">
		<h2 class="mb-6 text-3xl font-bold tracking-tight text-white md:text-5xl">
			{m['cta.title']()}
		</h2>
		<p class="mx-auto mb-10 max-w-2xl text-lg text-blue-100 md:text-xl">{m['cta.subtitle']()}</p>
		<div class="flex flex-col items-center justify-center gap-6 sm:flex-row">
			<a
				href="/contact"
				class="inline-flex items-center justify-center rounded-full bg-white px-10 py-4 text-lg font-bold text-primary transition-all hover:scale-105 hover:shadow-xl active:scale-95"
			>
				{m['cta.button']()}
			</a>
			<span class="font-medium text-white/80">{m['cta.call']()}</span>
		</div>
	</div>
</section>
