<script setup>
import { computed } from 'vue'
import AnimeCard from '@/components/AnimeCard.vue'
import { useAnimeRoulette } from '@/composables/useAnimeRoulette'
import WatchList from '@/components/WatchList.vue'

const { anime, loading, error, spin, cooldownLeft } = useAnimeRoulette()

const spinDisabled = computed(() => loading.value || cooldownLeft.value > 0)

const spinLabel = computed(() => {
  if (loading.value) {
    return 'Spinning...'
  }

  if (cooldownLeft.value > 0) {
    return `Cooldown ${cooldownLeft.value}s`
  }

  return 'SPIN 🎰'
})
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
                :disabled="spinDisabled"
                class="cursor-pointer rounded-full border border-slate-500/30 bg-slate-500/20 px-6 py-3 text-base font-black tracking-wide text-slate-100/90 hover:bg-slate-700/50 disabled:cursor-not-allowed disabled:opacity-70"
                @click="spin"
              >
                {{ spinLabel }}
              </button>
            </div>
            <p
              v-if="cooldownLeft > 0"
              class="mt-4 rounded-xl border border-b-amber-200/50 bg-slate-200/90 px-3 py-2 text-sm font-semibold text-slate-900/90"
            >
              Rate-limited. Try again in {{ cooldownLeft }}s.
            </p>
          </div>
          <AnimeCard
            :loading="loading"
            :error="error"
            :anime="anime"
          />
        </section>
        <WatchList />
      </div>
    </div>
  </main>
</template>
