<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { fade, fly, slide } from 'svelte/transition';
	import { onMount } from 'svelte';

	let mounted = false;

	onMount(() => {
		mounted = true;
	});

	const services = [
		{
			id: 'webdev',
			icon: '💻',
			title: () => m['services_page.list.webdev.title'](),
			desc: () => m['services_page.list.webdev.desc']()
		},
		{
			id: 'design',
			icon: '🎨',
			title: () => m['services_page.list.design.title'](),
			desc: () => m['services_page.list.design.desc']()
		},
		{
			id: 'ecommerce',
			icon: '🛍️',
			title: () => m['services_page.list.ecommerce.title'](),
			desc: () => m['services_page.list.ecommerce.desc']()
		},
		{
			id: 'seo',
			icon: '🚀',
			title: () => m['services_page.list.seo.title'](),
			desc: () => m['services_page.list.seo.desc']()
		}
	];

	const steps = [
		{
			num: '01',
			title: () => m['services_page.process.step1'](),
			desc: () => m['services_page.process.step1_desc']()
		},
		{
			num: '02',
			title: () => m['services_page.process.step2'](),
			desc: () => m['services_page.process.step2_desc']()
		},
		{
			num: '03',
			title: () => m['services_page.process.step3'](),
			desc: () => m['services_page.process.step3_desc']()
		},
		{
			num: '04',
			title: () => m['services_page.process.step4'](),
			desc: () => m['services_page.process.step4_desc']()
		}
	];
</script>

<svelte:head>
	<title>{m['services_page.title']()} | Company</title>
	<meta name="description" content={m['services_page.meta_desc']()} />
</svelte:head>

<div class="min-h-screen bg-white pb-20 dark:bg-background-dark">
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
						{m['services_page.title']()}
					</h1>
					<p
						in:fly={{ y: 20, duration: 800, delay: 200 }}
						class="mt-6 text-lg leading-8 text-gray-600 dark:text-gray-300"
					>
						{m['services_page.subtitle']()}
					</p>
				{/if}
			</div>
		</div>
	</section>

	<section class="mx-auto max-w-7xl px-6 py-12 lg:px-8">
		<div class="grid grid-cols-1 gap-8 md:grid-cols-2">
			{#each services as service, i}
				{#if mounted}
					<div
						in:fly={{ y: 30, duration: 800, delay: 300 + i * 100 }}
						class="group relative overflow-hidden rounded-3xl bg-gray-50 p-8 transition-all hover:-translate-y-1 hover:bg-white hover:shadow-xl dark:bg-surface-dark dark:hover:bg-gray-800"
					>
						<div
							class="mb-6 flex size-14 items-center justify-center rounded-2xl bg-white text-3xl shadow-sm dark:bg-gray-900"
						>
							{service.icon}
						</div>
						<h3 class="text-2xl font-bold text-gray-900 dark:text-white">
							{service.title()}
						</h3>
						<p class="mt-4 text-base leading-relaxed text-gray-600 dark:text-gray-300">
							{service.desc()}
						</p>
					</div>
				{/if}
			{/each}
		</div>
	</section>

	<section class="relative overflow-hidden bg-gray-900 py-24 text-white">
		<div
			class="absolute top-0 left-0 h-full w-full opacity-10"
			style="background-image: radial-gradient(#4f46e5 1px, transparent 1px); background-size: 32px 32px;"
		></div>

		<div class="relative z-10 mx-auto max-w-7xl px-6 lg:px-8">
			<div class="mb-16 text-center">
				<h2 class="text-3xl font-bold">{m['services_page.process.title']()}</h2>
			</div>

			<div class="grid grid-cols-1 gap-8 md:grid-cols-4">
				{#each steps as step, i}
					{#if mounted}
						<div in:fly={{ y: 20, duration: 800, delay: 600 + i * 150 }} class="relative">
							<!-- Connector Line (Desktop) -->
							{#if i !== steps.length - 1}
								<div
									class="absolute top-8 left-1/2 -z-10 hidden h-0.5 w-full bg-gray-700 md:block"
								></div>
							{/if}

							<div class="flex flex-col items-center text-center">
								<div
									class="mb-6 flex size-16 items-center justify-center rounded-full border-4 border-gray-900 bg-primary text-xl font-bold text-white"
								>
									{step.num}
								</div>
								<h3 class="mb-2 text-xl font-bold">{step.title()}</h3>
								<p class="text-sm text-gray-400">{step.desc()}</p>
							</div>
						</div>
					{/if}
				{/each}
			</div>
		</div>
	</section>

	<section class="mx-auto max-w-7xl px-6 py-24 lg:px-8">
		<div class="mb-16 text-center">
			<h2 class="text-3xl font-bold text-gray-900 dark:text-white">
				{m['services_page.pricing.title']()}
			</h2>
			<p class="mt-4 text-gray-600 dark:text-gray-300">
				{m['services_page.pricing.subtitle']()}
			</p>
		</div>

		<div class="grid grid-cols-1 gap-8 md:grid-cols-3">
			<div
				class="rounded-3xl border border-gray-200 bg-white p-8 shadow-sm transition-all hover:shadow-xl dark:border-gray-800 dark:bg-surface-dark"
			>
				<h3 class="text-lg font-semibold text-gray-900 dark:text-white">
					{m['services_page.pricing.basic.title']()}
				</h3>
				<div class="mt-4 flex items-baseline text-3xl font-bold text-gray-900 dark:text-white">
					{m['services_page.pricing.basic.price']()}
				</div>
				<ul class="mt-8 space-y-4 text-sm leading-6 text-gray-600 dark:text-gray-300">
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.basic.feature1']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.basic.feature2']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.basic.feature3']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.basic.feature4']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.basic.feature5']()}
					</li>
				</ul>
				<a
					href="/contact"
					class="mt-8 block rounded-md bg-primary/10 px-3 py-2 text-center text-sm font-semibold text-primary hover:bg-primary/20"
				>
					{m['services_page.cta.button']()}
				</a>
			</div>
			<div
				class="relative rounded-3xl border-2 border-primary bg-white p-8 shadow-xl dark:border-primary dark:bg-surface-dark"
			>
				<div
					class="absolute -top-5 left-1/2 -translate-x-1/2 rounded-full bg-primary px-4 py-1 text-xs font-semibold text-white"
				>
					POPULAR
				</div>
				<h3 class="text-lg font-semibold text-gray-900 dark:text-white">
					{m['services_page.pricing.pro.title']()}
				</h3>
				<div class="mt-4 flex items-baseline text-3xl font-bold text-gray-900 dark:text-white">
					{m['services_page.pricing.pro.price']()}
				</div>
				<ul class="mt-8 space-y-4 text-sm leading-6 text-gray-600 dark:text-gray-300">
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.pro.feature1']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.pro.feature2']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.pro.feature3']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.pro.feature4']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.pro.feature5']()}
					</li>
				</ul>
				<a
					href="/contact"
					class="mt-8 block rounded-md bg-primary px-3 py-2 text-center text-sm font-semibold text-white shadow-lg shadow-primary/30 hover:bg-primary/90"
				>
					{m['services_page.cta.button']()}
				</a>
			</div>

			<div
				class="rounded-3xl border border-gray-200 bg-white p-8 shadow-sm transition-all hover:shadow-xl dark:border-gray-800 dark:bg-surface-dark"
			>
				<h3 class="text-lg font-semibold text-gray-900 dark:text-white">
					{m['services_page.pricing.enterprise.title']()}
				</h3>
				<div class="mt-4 flex items-baseline text-3xl font-bold text-gray-900 dark:text-white">
					{m['services_page.pricing.enterprise.price']()}
				</div>
				<ul class="mt-8 space-y-4 text-sm leading-6 text-gray-600 dark:text-gray-300">
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.enterprise.feature1']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.enterprise.feature2']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.enterprise.feature3']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.enterprise.feature4']()}
					</li>
					<li class="flex gap-x-3">
						<span class="text-primary">✓</span>
						{m['services_page.pricing.enterprise.feature5']()}
					</li>
				</ul>
				<a
					href="/contact"
					class="mt-8 block rounded-md bg-primary/10 px-3 py-2 text-center text-sm font-semibold text-primary hover:bg-primary/20"
				>
					{m['services_page.cta.button']()}
				</a>
			</div>
		</div>
	</section>

	<!-- CTA Section -->
	<section class="mx-auto max-w-7xl px-6 pb-16 lg:px-8">
		<div
			class="relative isolate overflow-hidden rounded-3xl bg-gray-900 px-6 py-24 text-center shadow-2xl sm:px-16"
		>
			<h2 class="mx-auto max-w-2xl text-3xl font-bold tracking-tight text-white sm:text-4xl">
				{m['services_page.cta.title']()}
			</h2>
			<p class="mx-auto mt-6 max-w-xl text-lg leading-8 text-gray-300">
				{m['services_page.cta.text']()}
			</p>
			<div class="mt-10 flex items-center justify-center gap-x-6">
				<a
					href="/contact"
					class="rounded-md bg-white px-3.5 py-2.5 text-sm font-semibold text-gray-900 shadow-sm hover:bg-gray-100 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white"
				>
					{m['services_page.cta.button']()}
				</a>
			</div>
		</div>
	</section>
</div>
