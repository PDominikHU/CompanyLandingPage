<script lang="ts">
	import * as m from '$lib/paraglide/messages';
	import { page } from '$app/state';
	import { slide } from 'svelte/transition';
	import { setLocale, localizeHref, getLocale } from '$lib/paraglide/runtime.js';
	import ThemeSwitch from '$lib/components/ThemeSwitch.svelte';

	let isMobileMenuOpen = $state(false);

	function toggleMenu() {
		isMobileMenuOpen = !isMobileMenuOpen;
	}

	function closeMenu() {
		isMobileMenuOpen = false;
	}

	let currentLocale = $derived(getLocale());
	let isEnglish = $derived(currentLocale === 'en');

	function handleLanguageToggle() {
		const newLocale = isEnglish ? 'hu' : 'en';
		setLocale(newLocale);
		closeMenu();
	}
</script>

<nav
	class="sticky top-0 z-50 border-b border-gray-100 bg-white/90 backdrop-blur-md dark:border-gray-800 dark:bg-background-dark/95"
>
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
		<div class="flex h-16 items-center justify-between">
			<div class="shrink-0">
				<a href={localizeHref('/')} class="text-xl font-black text-primary" onclick={closeMenu}
					>LOGO</a
				>
			</div>

			<div class="hidden items-center space-x-2 md:flex">
				<a
					href={localizeHref('/services')}
					class="nav-link"
					class:active={page.url.pathname.includes('services')}
				>
					{m.services()}
					<span class="underline-animation"></span>
				</a>
				<a
					href={localizeHref('/portfolio')}
					class="nav-link"
					class:active={page.url.pathname.includes('portfolio')}
				>
					{m.portfolio()}
					<span class="underline-animation"></span>
				</a>
				<a
					href={localizeHref('/contact')}
					class="nav-link"
					class:active={page.url.pathname.includes('contact')}
				>
					{m.contact()}
					<span class="underline-animation"></span>
				</a>

				<button
					onclick={handleLanguageToggle}
					class="flex items-center justify-center rounded-md p-1 transition-transform duration-200 hover:scale-110 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-500"
					aria-label={isEnglish ? 'Váltás magyarra' : 'Switch to English'}
					title={isEnglish ? 'Váltás magyarra' : 'Switch to English'}
				>
					<img
						src={isEnglish ? '/images/flags/hungary.svg' : '/images/flags/uk.svg'}
						alt={isEnglish ? 'Magyar' : 'English'}
						class="h-6 w-6 rounded-sm object-cover shadow-sm"
					/>
				</button>

				<!-- Theme Toggle Lamp Cord -->
				<div class="relative ml-2 h-10 w-10">
					<ThemeSwitch />
				</div>
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
				<a
					href={localizeHref('/services')}
					class="mobile-link"
					class:active={page.url.pathname.includes('services')}
					onclick={closeMenu}>{m.services()}</a
				>
				<a
					href={localizeHref('/portfolio')}
					class="mobile-link"
					class:active={page.url.pathname.includes('portfolio')}
					onclick={closeMenu}>{m.portfolio()}</a
				>
				<a
					href={localizeHref('/contact')}
					class="mobile-link"
					class:active={page.url.pathname.includes('contact')}
					onclick={closeMenu}>{m.contact()}</a
				>

				<div class="my-4 border-t border-gray-100 dark:border-gray-800"></div>

				<div class="flex items-center justify-between px-2">
					<div class="flex items-center gap-4">
						<span class="text-sm font-medium text-gray-600 dark:text-gray-400">
							{isEnglish ? 'Language' : 'Nyelv'}
						</span>
						<button
							onclick={handleLanguageToggle}
							class="flex items-center justify-center rounded-md p-1 transition-transform duration-200 hover:scale-110 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-500"
							aria-label={isEnglish ? 'Váltás magyarra' : 'Switch to English'}
							title={isEnglish ? 'Váltás magyarra' : 'Switch to English'}
						>
							<img
								src={isEnglish ? '/images/flags/hungary.svg' : '/images/flags/uk.svg'}
								alt={isEnglish ? 'Magyar' : 'English'}
								class="h-6 w-6 rounded-sm object-cover shadow-sm"
							/>
						</button>
					</div>

					<!-- Mobile Theme Toggle (Simple Button) -->
					<div class="relative h-8 w-8">
						<ThemeSwitch variant="button" />
					</div>
				</div>
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
		color: var(--color-primary);
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
		background-color: var(--color-primary);
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
		border-bottom: 1px solid var(--color-background-light);
		color: #374151;
	}
	.mobile-link.active {
		color: var(--color-primary);
	}
	:global(.dark) .mobile-link {
		color: #ffffff;
		border-bottom-color: var(--color-surface-dark);
	}
	:global(.dark) .mobile-link.active {
		color: var(--color-primary);
	}
</style>
