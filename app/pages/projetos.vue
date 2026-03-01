<script setup lang="ts">
import projetos from "~/data/projetos.json";
</script>

<template>
  <AppHeader />
  <main class="bg-acres-cloud">
    <div class="mx-auto max-w-6xl px-4 py-14">
      <h1 class="font-heading text-4xl font-extrabold">Projetos</h1>
      <p class="mt-2 text-black/70">
        Conheça as iniciativas atuais da ACRES Sabará.
      </p>

      <div class="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <article
          v-for="p in projetos.items"
          :key="p.slug"
          class="rounded-2xl bg-white shadow-soft border border-black/5 p-6"
        >
          <div
            class="inline-flex text-xs font-semibold rounded-full px-3 py-1 bg-acres-yellow text-acres-ink"
          >
            {{ p.tag }}
          </div>

          <h2 class="mt-4 font-heading text-2xl font-extrabold">
            {{ p.title }}
          </h2>
          <p class="mt-2 text-black/70">{{ p.summary }}</p>

          <NuxtLink
            :to="`/projetos#${p.slug}`"
            class="mt-5 inline-flex text-sm font-semibold text-acres-blue hover:underline"
          >
            Ver detalhes
          </NuxtLink>
        </article>
      </div>
    </div>
  </main>
  <AppFooter />
</template>
