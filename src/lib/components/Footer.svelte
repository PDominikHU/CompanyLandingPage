<script lang="ts">
	import * as m from '$lib/paraglide/messages';
</script>

<footer class="mt-auto w-full bg-[#092330] pt-16 pb-8 text-sm text-gray-400">
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
		<div class="grid gap-12 md:grid-cols-2 lg:grid-cols-4">
			<div class="flex flex-col gap-6">
				<a href="/" class="text-2xl font-black text-white">LOGO</a>
				<p class="max-w-xs leading-relaxed">{m['footer.quote']()}</p>
			</div>

			<div>
				<h4 class="mb-6 font-bold tracking-wider text-white uppercase">{m['footer.links']()}</h4>
				<ul class="space-y-4">
					<li><a href="/" class="transition-colors hover:text-white">{m.home()}</a></li>
					<li><a href="/services" class="transition-colors hover:text-white">{m.services()}</a></li>
					<li>
						<a href="/portfolio" class="transition-colors hover:text-white">{m.portfolio()}</a>
					</li>
					<li>
						<a href="/" class="transition-colors hover:text-white">{m['footer.process']()}</a>
					</li>
				</ul>
			</div>

			<div>
				<h4 class="mb-6 font-bold tracking-wider text-white uppercase">
					{m['footer.further_information']()}
				</h4>
				<ul class="space-y-4">
					<li>
						<a href="/" class="transition-colors hover:text-white">{m['footer.reviews']()}</a>
					</li>
					<li><a href="/contact" class="transition-colors hover:text-white">{m.contact()}</a></li>
				</ul>
			</div>

			<div>
				<h4 class="mb-6 font-bold tracking-wider text-white uppercase">
					{m['footer.get_in_touch']()}
				</h4>
				<ul class="space-y-4">
					<li class="flex items-center gap-3">
						✉ <a href="mailto:info@example.com" class="transition-colors hover:text-white"
							>info@example.com</a
						>
					</li>
					<li class="flex items-center gap-3">📍 Pécs, Magyarország</li>
				</ul>
			</div>
		</div>

		<div
			class="mt-16 flex flex-col items-center justify-between gap-4 border-t border-gray-800 pt-8 md:flex-row"
		>
			<p class="text-xs">© 2025 {m['footer.rights']()}.</p>
			<div class="flex space-x-8 text-xs">
				<a href="/" class="transition-colors hover:text-white">{m['footer.privacy']()}</a>
				<a href="/" class="transition-colors hover:text-white">{m['footer.terms']()}</a>
			</div>
		</div>
	</div>
</footer>
