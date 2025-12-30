<script lang="ts">
	let { title, description } = $props();
</script>

<div
	class="rounded-xl border border-gray-100 bg-white p-6 shadow-sm transition-colors hover:border-primary/50 dark:border-gray-800 dark:bg-background-dark"
>
	<h3 class="text-lg font-bold text-gray-900 dark:text-white">{title}</h3>
	<p class="mt-2 text-sm text-gray-600 dark:text-gray-300">{description}</p>
</div>
