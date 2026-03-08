<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from "vue";

type HeroSlide = {
  id: number;
  title: string;
  subtitle?: string;
  description: string;
  image: string;
  ctaText?: string;
  ctaLink?: string;
  overlay?: string;
};

const props = withDefaults(
  defineProps<{
    slides: HeroSlide[];
    autoplay?: boolean;
    interval?: number;
  }>(),
  {
    autoplay: true,
    interval: 5000,
  },
);

const current = ref(0);
let timer: ReturnType<typeof setInterval> | null = null;

const hasSlides = computed(() => props.slides.length > 0);
const currentSlide = computed(() => props.slides[current.value]);

function nextSlide() {
  if (!hasSlides.value) return;
  current.value = (current.value + 1) % props.slides.length;
}

function prevSlide() {
  if (!hasSlides.value) return;
  current.value =
    (current.value - 1 + props.slides.length) % props.slides.length;
}

function goToSlide(index: number) {
  current.value = index;
  restartAutoplay();
}

function startAutoplay() {
  if (!props.autoplay || props.slides.length <= 1) return;
  stopAutoplay();
  timer = setInterval(() => {
    nextSlide();
  }, props.interval);
}

function stopAutoplay() {
  if (timer) {
    clearInterval(timer);
    timer = null;
  }
}

function restartAutoplay() {
  stopAutoplay();
  startAutoplay();
}

onMounted(() => {
  startAutoplay();
});

onBeforeUnmount(() => {
  stopAutoplay();
});
</script>

<template>
  <section
    class="relative overflow-hidden bg-slate-950 text-white shadow-2xl"
    @mouseenter="stopAutoplay"
    @mouseleave="startAutoplay"
  >
    <div v-if="hasSlides" class="relative h-120">
      <Transition name="fade" mode="out-in">
        <div :key="currentSlide?.id" class="absolute inset-0">
          <img
            :src="currentSlide?.image"
            :alt="currentSlide?.title"
            class="absolute inset-0 z-0 h-full w-full object-cover"
          />

          <div
            class="absolute inset-0 bg-gradient-to-r from-black/75 bg-gray/45 bg-gray-100/20"
            :style="{ backgroundColor: currentSlide?.overlay || 'transparent' }"
          />

          <div class="relative z-10 flex h-full items-center">
            <div class="mx-auto w-full max-w-6xl px-6 md:px-10">
              <div class="max-w-2xl">
                <p
                  v-if="currentSlide?.subtitle"
                  class="mb-3 inline-flex rounded-full p1-4 py-1 text-xs font-semibold uppercase tracking-[0.2em] backdrop-blur text-acres-yellow/90"
                >
                  {{ currentSlide?.subtitle }}
                </p>

                <h1 class="text-4xl font-extrabold leading-tight md:text-6xl">
                  {{ currentSlide?.title }}
                </h1>

                <p class="mt-5 text-base leading-7 text-white/85 md:text-lg">
                  {{ currentSlide?.description }}
                </p>

                <div
                  v-if="currentSlide?.ctaText && currentSlide.ctaLink"
                  class="mt-8"
                >
                  <NuxtLink
                    :to="currentSlide?.ctaLink"
                    class="inline-flex items-center rounded-full py-3 text-sm font-bold text-acres-blue/90 transition hover:scale-[1.02]"
                  >
                    {{ currentSlide?.ctaText }}
                  </NuxtLink>
                </div>
              </div>
            </div>
          </div>
        </div>
      </Transition>

      <div class="absolute bottom-6 left-1/2 z-20 flex -translate-x-1/2 gap-2">
        <button
          v-for="(slide, index) in slides"
          :key="slide.id"
          type="button"
          :aria-label="`Ir para slide ${index + 1}`"
          class="h-3 rounded-full transition-all"
          :class="
            index === current ? 'w-8  bg-acres-yellow' : 'w-3 bg-acres-blue'
          "
          @click="goToSlide(index)"
        />
      </div>
    </div>

    <div
      v-else
      class="flex h-105 items-center justify-center bg-slate-900 px-6 text-center text-white/70"
    >
      Nenhum slide configurado.
    </div>
  </section>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.45s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
