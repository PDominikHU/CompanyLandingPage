<script lang="ts">
    import * as m from "$lib/paraglide/messages";

</script>

<footer class="bg-[#092330] text-[#70828c] text-1rem">
    <div class="max-w-7xl mx-auto">
        <div class="grid md:grid-cols-4 gap-8">
            <div>
                <ul class="space-y-2">
                    <li><a href="/">Logo</a></li>
                    <li>{m["footer.quote"]()}</li>
                    <li>
                        <a href="/" class="hover:text-white transition-colors">Facebook</a>
                        <a href="/" class="hover:text-white transition-colors">Instagram</a>
                        <a href="/" class="hover:text-white transition-colors">Linkedin</a>
                    </li>
                </ul>
            </div>
            <div>
                <h4 class="text-white font-semibold mb-4">{m["footer.links"]()}</h4>
                <ul class="space-y-2">
                <li><a href="/" class="hover:text-white transition-colors">{m["footer.home"]()}</a></li>
                <li><a href="/about" class="hover:text-white transition-colors">{m["footer.services"]()}</a></li>
                <li><a href="/" class="hover:text-white transition-colors">{m["footer.process"]()}</a></li>
                <li><a href="/portfolio" class="hover:text-white transition-colors">{m["footer.portfolio"]()}</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-white font-semibold mb-4">További Információk</h4>
                <ul class="space-y-2">
                <li><a href="/" class="hover:text-white transition-colors">Vélemények</a></li>
                <li><a href="/about" class="hover:text-white transition-colors">Kapcsolat</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-white font-semibold mb-4">Lépj kapcsolatba</h4>
                <ul class="space-y-2">
                <li><a href="/" class="hover:text-white transition-colors">info@example.com</a></li>
                <li><a href="/about" class="hover:text-white transition-colors">SZABÓ TELEFON</a></li>
                <li><a href="/about" class="hover:text-white transition-colors">Pécs, Magyarország</a></li>
                </ul>
            </div>
            <div class="w-full h-px bg-[#233742] rounded col-span-4 my-4"></div>
            <div class="col-span-4 flex justify-between">
                <div>@2025 Minden jog fenntartva.</div>
                <div class="flex justify between space-x-6">
                    <div><a href="/">Adatvédelem</a></div>
                    <div><a href="/">Felhasználási feltételek</a></div>
                </div>
            </div>
        </div>
    </div>
</footer>