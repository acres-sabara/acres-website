<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";
import quotes from "~/data/quotes.json";

const current = ref(0);

let timer: ReturnType<typeof setInterval> | null = null;

function nextQuote() {
  current.value = (current.value + 1) % quotes.length;
}

onMounted(() => {
  timer = setInterval(nextQuote, 6000);
});

onBeforeUnmount(() => {
  if (timer) clearInterval(timer);
});
</script>

<template>
  <section class="py-20 bg-gray-50">
    <div class="max-w-4xl mx-auto px-6 text-center min-h-28">
      <transition name="fade" mode="out-in">
        <div :key="current">
          <blockquote
            class="font-sans text-base md:text-base italic text-acres-blue leading-relaxed"
          >
            “{{ quotes[current]?.quote }}”
          </blockquote>

          <p class="mt-6 text-lg font-semibold text-acres-yellow">
            — {{ quotes[current]?.author }}
          </p>
        </div>
      </transition>
    </div>
  </section>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
