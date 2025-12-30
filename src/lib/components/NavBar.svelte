<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';
	import { slide } from 'svelte/transition';

	let isMobileMenuOpen = $state(false);

	function toggleMenu() {
		isMobileMenuOpen = !isMobileMenuOpen;
	}

	function closeMenu() {
		isMobileMenuOpen = false;
	}

	function handleOffer() {
		closeMenu();
		goto('/contact');
	}
</script>

<nav
	class="sticky top-0 z-50 border-b border-gray-100 bg-white/90 backdrop-blur-md transition-colors dark:border-gray-800 dark:bg-background-dark/95"
>
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
		<div class="flex h-16 items-center justify-between">
			<div class="shrink-0">
				<a href="/" class="text-xl font-black text-primary" onclick={closeMenu}>LOGO</a>
			</div>

			<div class="hidden items-center space-x-2 md:flex">
				<a href="/services" class="nav-link" class:active={$page.url.pathname.includes('services')}>
					{m.services()}
					<span class="underline-animation"></span>
				</a>
				<a
					href="/portfolio"
					class="nav-link"
					class:active={$page.url.pathname.includes('portfolio')}
				>
					{m.portfolio()}
					<span class="underline-animation"></span>
				</a>
				<a href="/contact" class="nav-link" class:active={$page.url.pathname.includes('contact')}>
					{m.contact()}
					<span class="underline-animation"></span>
				</a>

				<button
					class="ml-4 cursor-pointer rounded-lg bg-primary px-6 py-2.5 text-sm font-bold text-white transition-all hover:scale-105 hover:bg-primary/90 active:scale-95"
					onclick={handleOffer}
				>
					{m['navbar.ask_offer']()}
				</button>
			</div>

			<div class="flex md:hidden">
				<button
					type="button"
					aria-label="Toggle Menu"
					class="relative flex size-10 cursor-pointer items-center justify-center rounded-md text-gray-600 dark:text-gray-200"
					onclick={toggleMenu}
				>
					<div class="flex w-6 flex-col items-end gap-1.5">
						<span
							class="h-0.5 bg-current transition-all duration-300 {isMobileMenuOpen
								? 'w-6 translate-y-2 rotate-45'
								: 'w-6'}"
						></span>
						<span
							class="h-0.5 bg-current transition-all duration-300 {isMobileMenuOpen
								? 'opacity-0'
								: 'w-4'}"
						></span>
						<span
							class="h-0.5 bg-current transition-all duration-300 {isMobileMenuOpen
								? 'w-6 -translate-y-2 -rotate-45'
								: 'w-5'}"
						></span>
					</div>
				</button>
			</div>
		</div>
	</div>

	{#if isMobileMenuOpen}
		<div
			transition:slide={{ duration: 300 }}
			class="overflow-hidden border-b border-gray-100 bg-white md:hidden dark:border-gray-800 dark:bg-background-dark"
		>
			<div class="flex flex-col gap-1 px-4 pt-2 pb-6">
				<a href="/services" class="mobile-link" onclick={closeMenu}>{m.services()}</a>
				<a href="/portfolio" class="mobile-link" onclick={closeMenu}>{m.portfolio()}</a>
				<a href="/contact" class="mobile-link" onclick={closeMenu}>{m.contact()}</a>

				<button
					class="mt-4 w-full cursor-pointer rounded-lg bg-primary py-4 text-base font-bold text-white shadow-lg shadow-primary/20"
					onclick={handleOffer}
				>
					{m['navbar.ask_offer']()}
				</button>
			</div>
		</div>
	{/if}
</nav>

<style>
	.nav-link {
		position: relative;
		padding: 0.5rem 1rem;
		font-size: 0.875rem;
		font-weight: 600;
		color: #4b5563;
		transition: color 0.2s;
	}
	:global(.dark) .nav-link {
		color: #d1d5db;
	}
	.nav-link:hover,
	.nav-link.active {
		color: #136dec;
	}
	:global(.dark) .nav-link:hover,
	:global(.dark) .nav-link.active {
		color: #ffffff;
	}

	.underline-animation {
		position: absolute;
		bottom: 0;
		left: 1rem;
		right: 1rem;
		height: 2px;
		background-color: #136dec;
		transform: scaleX(0);
		transition: transform 0.3s ease-out;
		transform-origin: left;
	}
	.nav-link:hover .underline-animation,
	.nav-link.active .underline-animation {
		transform: scaleX(1);
	}

	.mobile-link {
		display: block;
		padding: 1rem 0;
		font-size: 1.125rem;
		font-weight: 700;
		border-bottom: 1px solid #f3f4f6;
		color: #374151;
	}
	:global(.dark) .mobile-link {
		color: #ffffff;
		border-bottom-color: #1f2937;
	}
</style>
