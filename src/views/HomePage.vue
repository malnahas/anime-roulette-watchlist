<script setup>
import { ref } from 'vue'
import AnimeCard from '@/components/AnimeCard.vue'

const loading = ref(false)
const error = ref('')

const spin = () => {
  if (error.value.length > 0) error.value = ''
  else error.value = 'Something wrong'
}
</script>

<template>
  <main
    class="min-h-screen bg-[radial-gradient(circle_at_15%_20%,#334200,transparent_40%),radial-gradient(circle_at_85%_0%,#0f800e,transparent_28%),linear-gradient(160deg,#011800,#0f172a,#111827)] px-4 py-8 text-slate-300 sm:px-6 lg:px-8"
  >
    <div class="mx-auto max-w-7xl">
      <header class="mb-8">
        <p class="text-xs font-semibold tracking-[0.3em] text-cyan-800/100 uppercase">Project #4</p>
        <h1 class="mt-2 text-4xl font-black text-white sm:text-5xl">Anime Roulette Machine</h1>
        <p class="mt-2 max-w-3xl text-sm text-slate-200/50 sm:text-base">
          Spin the reel, request a random anime from Jinkan with VueUse useFech, and learn how REST
          APIs signal rate limiting with HTTP 429.
        </p>
      </header>

      <div class="grid gap-6 lg:grid-cols-[1.2fr_0.8fr]">
        <section class="space-y-5">
          <div
            class="rounded-3xl border border-slate-500/60 bg-slate-600 p-5 shadow-2xl shadow-slate-800 backdrop-blur-sm"
          >
            <div class="flex flex-col gap-3 sm:flex-row sm:items-center sm:justify-between">
              <div>
                <h2 class="text-xl font-bold text-green-300/50">Roulette</h2>
                <p class="text-sm text-slate-200/50">
                  Pull the lever for the next random anime recommendation.
                </p>
              </div>
              <button
                type="button"
                class="cursor-pointer rounded-full border border-slate-500/30 bg-slate-500/20 px-6 py-3 text-base font-black tracking-wide text-slate-100/90 hover:bg-slate-700/50"
                @click="spin"
              >
                Spin
              </button>
            </div>
          </div>
          <AnimeCard
            :loading="loading"
            :error="error"
          />
        </section>
      </div>
    </div>
  </main>
</template>
