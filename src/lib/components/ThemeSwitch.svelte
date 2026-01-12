<script lang="ts">
	import { onMount } from 'svelte';

	let isDark = $state(false);
	let isPulling = $state(false);

	function toggleTheme(event?: MouseEvent) {
		const html = document.documentElement;
		const isDarkNow = html.classList.contains('dark');

		if (!document.startViewTransition) {
			updateTheme(!isDarkNow);
			return;
		}

		let x = window.innerWidth / 2;
		let y = window.innerHeight / 2;

		if (event) {
			x = event.clientX;
			y = event.clientY;
		} else {
			const cordKnob = document.querySelector('.theme-knob');
			if (cordKnob) {
				const rect = cordKnob.getBoundingClientRect();
				x = rect.left + rect.width / 2;
				y = rect.top + rect.height / 2;
			} else {
				x = window.innerWidth - 80;
				y = 80;
			}
		}

		const endRadius = Math.hypot(
			Math.max(x, window.innerWidth - x),
			Math.max(y, window.innerHeight - y)
		);

		const transition = document.startViewTransition(async () => {
			await updateTheme(!isDarkNow);
		});

		transition.ready.then(() => {
			const clipPath = [`circle(0px at ${x}px ${y}px)`, `circle(${endRadius}px at ${x}px ${y}px)`];
			document.documentElement.animate(
				{
					clipPath: isDarkNow ? [...clipPath].reverse() : clipPath
				},
				{
					duration: 500,
					easing: 'ease-in-out',
					pseudoElement: isDarkNow ? '::view-transition-old(root)' : '::view-transition-new(root)'
				}
			);
		});
	}

	async function updateTheme(dark: boolean) {
		const html = document.documentElement;
		if (dark) {
			html.classList.add('dark');
			localStorage.setItem('theme', 'dark');
			isDark = true;
		} else {
			html.classList.remove('dark');
			localStorage.setItem('theme', 'light');
			isDark = false;
		}
	}

	function handleMouseDown() {
		isPulling = true;
	}

	function handleMouseUp() {
		if (isPulling) {
			isPulling = false;
			toggleTheme();
		}
	}

	onMount(() => {
		if (typeof window !== 'undefined') {
			const savedTheme = localStorage.getItem('theme');
			const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

			if (savedTheme === 'dark' || (!savedTheme && prefersDark)) {
				document.documentElement.classList.add('dark');
				isDark = true;
			} else {
				document.documentElement.classList.remove('dark');
				isDark = false;
			}
		}
	});

	let { variant = 'cord' } = $props<{ variant?: 'cord' | 'button' }>();
</script>

{#if variant === 'cord'}
	<div class="relative z-50 ml-4 hidden md:block">
		<div
			class="absolute left-1/2 w-0.5 origin-top bg-gray-400 transition-all duration-300 dark:bg-gray-600"
			style="height: {isPulling ? '60px' : '40px'}; top: -20px; transform: translateX(-50%);"
		></div>

		<button
			class="theme-knob absolute left-1/2 box-content h-6 w-6 -translate-x-1/2 rounded-full border-2 border-gray-300 bg-white shadow-md transition-all duration-300 outline-none hover:bg-gray-100 dark:border-gray-600 dark:bg-gray-800 dark:hover:bg-gray-700"
			style="top: {isPulling ? '40px' : '20px'};"
			onmousedown={handleMouseDown}
			onmouseup={handleMouseUp}
			onmouseleave={() => (isPulling = false)}
			aria-label="Toggle Theme"
		>
			<span class="flex h-full w-full items-center justify-center text-xs">
				{#if isDark}
					🌙
				{:else}
					☀️
				{/if}
			</span>
		</button>
	</div>
{:else}
	<button
		onclick={(e) => toggleTheme(e)}
		class="flex h-full w-full items-center justify-center rounded-md p-1 transition-transform duration-200 hover:scale-110 focus:ring-2 focus:ring-primary focus:outline-none"
		aria-label="Toggle Theme"
	>
		<span class="text-xl">
			{#if isDark}
				🌙
			{:else}
				☀️
			{/if}
		</span>
	</button>
{/if}
