<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import nav from "@/data/nav.json";

const isScrolled = ref(false);

const onScroll = () => {
  isScrolled.value = window.scrollY > 8;
};

onMounted(() => {
  onScroll();
  window.addEventListener("scroll", onScroll, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener("scroll", onScroll);
});
</script>

<template>
  <header
    :class="[
      'inset-x-0 transition-all duration-300 max-h-24',
      isScrolled
        ? 'bg-white/95 shadow-md backdrop-blur border-b border-black/5'
        : 'bg-white/80 backdrop-blur border-b border-black/5',
    ]"
  >
    <div class="mx-auto max-w-7xl px-4">
      <div
        :class="[
          'flex items-center justify-between',
          isScrolled ? 'py-3' : 'py-4',
        ]"
      >
        <!-- LOGO + TEXTO -->
        <NuxtLink to="/" class="flex items-center gap-3">
          <img
            src="/logo.png"
            alt="ACRES Sabará"
            class="h-15 w-auto object-contain"
          />

          <div class="leading-tight">
            <div
              class="text-2xl"
              style="font-family: Agbalumo, cursive; color: #ffde59"
            >
              SABARÁ
            </div>

            <div
              class="text-xs tracking-wide"
              style="font-family: Amaranth, sans-serif; color: #38b6ff"
            >
              Associação Cultural Recreativa Esportiva
            </div>
          </div>
        </NuxtLink>

        <!-- MENU -->
        <nav
          class="hidden md:flex items-center gap-8 text-sm font-semibold tracking-wide text-black/70 mr-5"
        >
          <NuxtLink
            v-for="item in nav.items"
            :key="item.to"
            :to="item.to"
            class="relative py-2 hover:text-black transition"
            active-class="text-black"
          >
            {{ item.label }}
            <span
              class="pointer-events-none absolute left-0 right-0 -bottom-0.5 h-0.5 scale-x-0 bg-yellow-400 transition-transform duration-200"
            />
          </NuxtLink>
        </nav>

        <!-- BOTÃO MOBILE (depois ligamos o menu) -->
        <button
          class="inline-flex md:hidden items-center justify-center rounded-xl p-2 ring-1 ring-black/10 hover:bg-black/5 transition"
          aria-label="Abrir menu"
          type="button"
        >
          <svg
            class="h-6 w-6 text-black/70"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M4 6h16M4 12h16M4 18h16"
            />
          </svg>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
/* Sublinhado aparece no hover e no link ativo */
a:hover > span,
a.router-link-active > span {
  transform: scaleX(1);
}
</style>
