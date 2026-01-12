<script lang="ts">
	let x = $state(0);
	let y = $state(0);

	function handleMouseMove(event: MouseEvent) {
		x = event.clientX;
		y = event.clientY;
	}
</script>

<svelte:window onmousemove={handleMouseMove} />

<div
	class="pointer-events-none fixed inset-0 z-30 opacity-40 transition-opacity duration-300 dark:hidden"
	style="background: radial-gradient(600px circle at {x}px {y}px, rgba(99, 102, 241, 0.15), transparent 80%);"
></div>

<div
	class="pointer-events-none fixed inset-0 z-30 hidden opacity-30 transition-opacity duration-300 dark:block"
	style="background: radial-gradient(600px circle at {x}px {y}px, rgba(99, 102, 241, 0.15), transparent 80%);"
></div>
