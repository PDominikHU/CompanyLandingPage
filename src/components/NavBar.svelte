<script lang="ts">
    import * as m from "$lib/paraglide/messages";
    import { goto } from "$app/navigation";

    function handleOffer() {
        goto("/");
    }

</script>

<nav class="bg-white/80 backdrop-blur-md border-b border-sky-100 sticky top-0 z-50 shadow-sm">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-16">
            <div>
                <a href="/">Logo</a>
            </div>
            <div class="hidden md:flex items-center space-x-10 ml-auto">
                <a href="/services" class="nav-link">
                    {m["navbar.services"]()}
                    <span class="underline-animation"></span>
                </a>

                <a href="/portfolio" class="nav-link">
                    {m["navbar.portfolio"]()}
                    <span class="underline-animation"></span>
                </a>

                <a href="/about" class="nav-link">
                    {m["navbar.about"]()}
                    <span class="underline-animation"></span>
                </a>

                <a href="/contact" class="nav-link">
                    {m["navbar.contact"]()}
                    <span class="underline-animation"></span>
                </a>
                <button class="w-half px-5 py-2 text-1rem font-medium text-white bg-gradient-to-r from-sky-500 to-blue-600 rounded-lg hover:from-sky-600 hover:to-blue-700 transition-all duration-300"
                    on:click={handleOffer}
                >
                    {m["navbar.ask_offer"]()}
                </button>
            </div>
        </div>
    </div>
</nav>

<style>
    .nav-link {
      position: relative;
      padding: 0.5rem 1rem;
      font-size: 1rem;
      font-weight: 500;
      color:#000000;
      transition: color 0.2s;
    }

    .nav-link:hover {
      color: #0284c7;
    }

    .underline-animation {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 2px;
      background: linear-gradient(to right, #0ea5e9, #2563eb);
      transition: width 0.3s ease-out;
    }
  
    .nav-link:hover .underline-animation {
      width: 100%;
    }
</style>