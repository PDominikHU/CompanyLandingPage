<script lang="ts">
	let { name, job, pic } = $props();
</script>

<div class="text-center">
	<img class="mx-auto h-32 w-32 rounded-full object-cover" alt={name} src={pic} />
	<h3 class="mt-4 text-lg font-bold text-gray-900 dark:text-white">{name}</h3>
	<p class="font-medium text-primary">{job}</p>
</div>
