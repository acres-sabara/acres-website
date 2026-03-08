<script setup lang="ts">
import cards from "~/data/homeHighlights.json";

type HighlightCard = {
  title: string;
  description: string;
  image: string;
  link: string;
};
</script>

<template>
  <section class="bg-white">
    <div class="max-w-5xl mx-auto min-h-80">
      <div class="grid md:grid-cols-3">
        <div
          v-for="card in cards"
          :key="card?.title"
          class="flex-1 items-center place-items-center bg-white text-center min-h-80 transition"
        >
          <img
            :src="card?.image"
            :alt="card?.title"
            class="h-24 mx-auto mt-10 mb-6 object-contain"
          />

          <h3 class="text-lg font-semibold mb-2">
            {{ card?.title }}
          </h3>

          <p class="text-gray-600 mb-6 text-sm">
            {{ card?.description }}
          </p>

          <NuxtLink
            :to="card.link"
            class="text-acres-blue font-semibold hover:underline"
          >
            Saiba mais
          </NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>
