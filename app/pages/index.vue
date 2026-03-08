<script setup>
import heroSlides from "~/data/hero-home.json";
</script>

<template>
  <div class="min-h-screen bg-acres-cloud">
    <main class="mx-auto max-w-6xl">
      <HeroCarousel :slides="heroSlides" :autoplay="true" :interval="6000" />
      <HomeHighlights />
    </main>
  </div>
</template>
