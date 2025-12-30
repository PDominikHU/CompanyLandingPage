<script lang="ts">
	let { title, description, icon } = $props();
</script>

<div
	class="flex flex-col items-center rounded-xl border border-gray-100 bg-white p-6 text-center shadow-sm transition-colors hover:border-primary/50 dark:border-gray-800 dark:bg-background-dark"
>
	<div
		class="mb-4 flex size-12 items-center justify-center rounded-full bg-primary/10 text-xl text-primary"
	>
		<span>{icon}</span>
	</div>

	<h3 class="min-h-1 text-lg leading-tight font-bold text-gray-900 dark:text-white">{title}</h3>
	<p class="mt-2 text-sm leading-relaxed text-gray-600 dark:text-gray-300">{description}</p>
</div>
