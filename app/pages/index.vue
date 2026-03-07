<template>
  <div class="min-h-screen bg-acres-cloud">
    <main class="mx-auto max-w-6xl px-10 py-16">
      <div class="grid gap-10 md:grid-cols-2 items-center">
        <div>
          <h1
            class="font-heading text-4xl md:text-5xl font-extrabold leading-tight"
          >
            Cultura, esporte e comunidade em movimento.
          </h1>
          <p class="mt-4 text-black/70 text-lg">
            A ACRES Sabará promove ações culturais, recreativas e esportivas com
            impacto real no bairro.
          </p>

          <div class="mt-8 flex gap-3">
            <a
              class="rounded-xl px-5 py-3 bg-acres-blue text-white font-semibold shadow-soft hover:opacity-95"
              href="#acoes"
            >
              Ver ações
            </a>
            <a
              class="rounded-xl px-5 py-3 bg-acres-yellow text-acres-ink font-semibold hover:opacity-95"
              href="#contato"
            >
              Falar com a ACRES
            </a>
          </div>
        </div>

        <div class="rounded-2xl bg-white shadow-soft p-6">
          <div class="text-sm font-semibold text-black/60">Destaque</div>
          <div class="mt-2 font-heading text-2xl font-extrabold">
            Próximo evento
          </div>
          <p class="mt-2 text-black/70">
            Em breve você vai preencher isso via <code>data/events.json</code>.
          </p>
          <div
            class="mt-4 h-40 rounded-xl bg-acres-cloud border border-black/5"
          />
        </div>
      </div>
    </main>
  </div>
</template>
