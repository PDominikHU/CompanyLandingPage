<script lang="ts">
	import { fly } from 'svelte/transition';
	import * as m from '$lib/paraglide/messages';

	let formStatus = $state<'idle' | 'submitting' | 'success' | 'error'>('idle');
	let errorMessage = $state('');

	const cls = {
		input:
			'w-full rounded-md border-0 bg-gray-50/50 px-4 py-3 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-primary dark:bg-surface-dark dark:text-white dark:ring-gray-700 dark:focus:ring-primary',
		label: 'block mb-2 text-sm font-medium text-gray-900 dark:text-white',
		iconBox:
			'flex h-12 w-12 shrink-0 items-center justify-center rounded-lg bg-primary/10 text-primary'
	};

	async function handleSubmit(event: SubmitEvent) {
		formStatus = 'submitting';
		const form = event.target as HTMLFormElement;

		try {
			const response = await fetch('https://formspree.io/f/xvzgljpy', {
				method: 'POST',
				body: new FormData(form),
				headers: { Accept: 'application/json' }
			});

			if (response.ok) {
				formStatus = 'success';
				form.reset();
				setTimeout(() => (formStatus = 'idle'), 5000);
			} else {
				const data = await response.json();

				// MEGOLDÁS: Definiáljuk a hiba típusát 'any' helyett
				errorMessage =
					data.errors?.map((error: { message: string }) => error.message).join(', ') ||
					(m['contactPage.errorMsg']?.() ?? 'Hiba történt.');
				formStatus = 'error';
			}
		} catch {
			formStatus = 'error';
			errorMessage = m['contactPage.errorMsg']?.() ?? 'Hálózati hiba.';
		}
	}
</script>

<section
	id="contact"
	class="relative flex flex-1 flex-col justify-center overflow-hidden border-t border-gray-100 bg-white py-20 dark:border-gray-800 dark:bg-surface-dark"
>
	<div class="relative mx-auto max-w-6xl px-4 lg:grid lg:grid-cols-2 lg:gap-16">
		<div class="mb-12 flex flex-col justify-center lg:mb-0">
			<h2 class="text-3xl font-bold text-gray-900 sm:text-4xl dark:text-white">
				{m['contactPage.title']?.() ?? 'Lépjünk kapcsolatba!'}
			</h2>
			<p class="mt-4 text-lg text-gray-600 dark:text-gray-300">
				{m['contactPage.subtitle']?.() ?? 'Kérdésed van? Projektet indítanál? Írj bátran!'}
			</p>

			<ul class="mt-10 space-y-6">
				<li class="flex items-center gap-4">
					<div class={cls.iconBox}>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor"
							class="size-6"
							><path
								stroke-linecap="round"
								stroke-linejoin="round"
								d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75"
							/></svg
						>
					</div>
					<a
						href="mailto:hello@company.com"
						class="text-lg font-semibold hover:text-primary dark:text-white">hello@company.com</a
					>
				</li>
				<li class="flex items-center gap-4">
					<div class={cls.iconBox}>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor"
							class="size-6"
							><path
								stroke-linecap="round"
								stroke-linejoin="round"
								d="M2.25 6.75c0 8.284 6.716 15 15 15h2.25a2.25 2.25 0 0 0 2.25-2.25v-1.372c0-.516-.351-.966-.852-1.091l-4.423-1.106c-.44-.11-.902.055-1.173.417l-.97 1.293c-.282.376-.769.542-1.21.38a12.035 12.035 0 0 1-7.143-7.143c-.162-.441.004-.928.38-1.21l1.293-.97c.363-.271.527-.734.417-1.173L6.963 3.102a1.125 1.125 0 0 0-1.091-.852H4.5A2.25 2.25 0 0 0 2.25 4.5v2.25Z"
							/></svg
						>
					</div>
					<a
						href="tel:+36204026075"
						class="text-lg font-semibold hover:text-primary dark:text-white">+36 20 402 6075</a
					>
				</li>
			</ul>
		</div>

		<form
			onsubmit={handleSubmit}
			class="grid gap-6 rounded-2xl bg-white p-8 shadow-lg ring-1 ring-gray-900/5 dark:bg-background-dark dark:ring-gray-700"
		>
			<div class="grid gap-6 sm:grid-cols-2">
				<label class="block">
					<span class={cls.label}>{m['contactPage.nameLabel']?.() ?? 'Név'}</span>
					<input
						type="text"
						name="name"
						required
						class={cls.input}
						placeholder={m['contactPage.namePlaceholder']?.() ?? 'Teljes név'}
					/>
				</label>

				<label class="block">
					<span class={cls.label}>{m['contactPage.phoneLabel']?.() ?? 'Telefonszám'}</span>
					<input
						type="tel"
						name="phone"
						class={cls.input}
						placeholder={m['contactPage.phonePlaceholder']?.() ?? '+36 20 123 4567'}
					/>
				</label>
			</div>

			<label class="block">
				<span class={cls.label}>{m['contactPage.emailLabel']?.() ?? 'Email cím'}</span>
				<input
					type="email"
					name="email"
					required
					class={cls.input}
					placeholder={m['contactPage.emailPlaceholder']?.() ?? 'pelda@email.com'}
				/>
			</label>

			<label class="block">
				<span class={cls.label}>{m['contactPage.messageLabel']?.() ?? 'Üzenet'}</span>
				<textarea
					name="message"
					rows="4"
					required
					class={cls.input}
					placeholder={m['contactPage.messagePlaceholder']?.() ?? 'Miben segíthetünk?'}
				></textarea>
			</label>

			<button
				type="submit"
				disabled={formStatus !== 'idle'}
				class="mt-2 flex w-full items-center justify-center gap-2 rounded-lg bg-primary py-3 font-bold text-white transition hover:bg-primary/90 disabled:opacity-70"
			>
				{#if formStatus === 'submitting'}
					<div
						class="h-5 w-5 animate-spin rounded-full border-2 border-white/30 border-t-white"
					></div>
					{m['contactPage.btnSending']?.() ?? 'Küldés...'}
				{:else if formStatus === 'success'}
					✓ {m['contactPage.btnSent']?.() ?? 'Elküldve'}
				{:else}
					{m['contactPage.btnSubmit']?.() ?? 'Üzenet küldése'}
				{/if}
			</button>

			{#if formStatus === 'success' || formStatus === 'error'}
				<p
					in:fly={{ y: 10 }}
					class="text-center text-sm font-medium {formStatus === 'success'
						? 'text-green-600'
						: 'text-red-600'}"
				>
					{formStatus === 'success'
						? (m['contactPage.successMsg']?.() ?? 'Köszönjük! Hamarosan keresünk.')
						: errorMessage}
				</p>
			{/if}
		</form>
	</div>
</section>
