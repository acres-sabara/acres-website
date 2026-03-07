<template>
  <div class="min-h-screen bg-gray-100 text-acres-ink py-20">
    <AppHeader class="max-w-5xl mx-auto" />
    <main class="max-w-5xl mx-auto py-4">
      <slot />
    </main>

    <AppFooter
      class="bg-white max-w-5xl mx-auto max-h-24 transition-all duration-300"
    />
  </div>
</template>
