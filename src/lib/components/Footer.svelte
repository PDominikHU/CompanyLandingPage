<script lang="ts">
	import * as m from '$lib/paraglide/messages';
</script>

<footer class="text-1rem bg-[#092330] text-[#70828c]">
	<div class="mx-auto max-w-7xl">
		<div class="grid gap-8 md:grid-cols-4">
			<div>
				<ul class="space-y-2">
					<li><a href="/">Logo</a></li>
					<li>{m['footer.quote']()}</li>
					<li>
						<a href="/" class="transition-colors hover:text-white">Facebook</a>
						<a href="/" class="transition-colors hover:text-white">Instagram</a>
						<a href="/" class="transition-colors hover:text-white">Linkedin</a>
					</li>
				</ul>
			</div>
			<div>
				<h4 class="mb-4 font-semibold text-white">{m['footer.links']()}</h4>
				<ul class="space-y-2">
					<li><a href="/" class="transition-colors hover:text-white">{m.home()}</a></li>
					<li>
						<a href="/about" class="transition-colors hover:text-white">{m.services()}</a>
					</li>
					<li>
						<a href="/" class="transition-colors hover:text-white">{m['footer.process']()}</a>
					</li>
					<li>
						<a href="/portfolio" class="transition-colors hover:text-white">{m.portfolio()}</a>
					</li>
				</ul>
			</div>
			<div>
				<h4 class="mb-4 font-semibold text-white">További Információk</h4>
				<ul class="space-y-2">
					<li><a href="/" class="transition-colors hover:text-white">Vélemények</a></li>
					<li><a href="/contact" class="transition-colors hover:text-white">{m.contact()}</a></li>
				</ul>
			</div>
			<div>
				<h4 class="mb-4 font-semibold text-white">Lépj kapcsolatba</h4>
				<ul class="space-y-2">
					<li><a href="/" class="transition-colors hover:text-white">info@example.com</a></li>
					<li><a href="/about" class="transition-colors hover:text-white">SZABÓ TELEFON</a></li>
					<li>
						<a href="/about" class="transition-colors hover:text-white">Pécs, Magyarország</a>
					</li>
				</ul>
			</div>
			<div class="col-span-4 my-4 h-px w-full rounded bg-[#233742]"></div>
			<div class="col-span-4 flex justify-between">
				<div>@2025 Minden jog fenntartva.</div>
				<div class="justify between flex space-x-6">
					<div><a href="/">Adatvédelem</a></div>
					<div><a href="/">Felhasználási feltételek</a></div>
				</div>
			</div>
		</div>
	</div>
</footer>
