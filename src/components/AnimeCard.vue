<script setup>
const props = defineProps({
  anime: {
    type: Object,
    default: null,
  },
  loading: {
    type: Boolean,
    default: false,
  },
  error: {
    type: String,
    default: '',
  },
  inWatchlist: {
    type: Boolean,
    default: false,
  },
})
</script>

<template>
  <section
    class="shadow-slate-850/30 rounded-3xl border border-slate-500/80 bg-slate-600/70 p-5 shadow-2xl backdrop-blur-sm"
  >
    <div
      v-if="props.loading"
      class="space-y-4"
    >
      <div class="flex items-center gap-3 text-cyan-500/90">
        <div
          class="h-5 w-5 animate-spin rounded-full border-2 border-cyan-600/90 border-t-transparent"
        ></div>
        <p class="font-semibold tracking-wide">Shuffling anime reels...</p>
      </div>

      <div class="grid grid-cols-3 gap-2">
        <div class="h-3 animate-pulse rounded bg-slate-400/30"></div>
        <div class="h-3 animate-pulse rounded bg-slate-400/30"></div>
        <div class="h-3 animate-pulse rounded bg-slate-400/30"></div>
      </div>
      <div class="h-72 animate-pulse rounded-2xl bg-slate-500/60"></div>
    </div>

    <div
      v-else-if="error"
      class="rounded-2xl border border-red-500/90 bg-red-400/30 p-4 text-red-100"
    >
      <h3 class="text-lg font-semibold">Spin failed</h3>
      <p class="mt-2 text-sm text-red-100/90">{{ error }}</p>
    </div>

    <div
      v-else
      class="rounded-2xl border border-slate-500/60 bg-slate-700/50 p-6 text-center text-slate-300"
    >
      Pull the lever to request your first random anime.
    </div>
  </section>
</template>
