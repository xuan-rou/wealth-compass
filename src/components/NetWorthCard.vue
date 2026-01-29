<script setup lang="ts">
defineProps<{
  amount: string
}>()
</script>

<template>
  <div
    class="shadow-dreamy relative overflow-hidden rounded-4xl border border-white/40 bg-white/20 p-6 backdrop-blur-md"
  >
    <!-- Decorative background circle -->
    <div
      class="absolute -top-10 -right-10 h-40 w-40 rounded-full bg-linear-to-br from-white/30 to-transparent blur-2xl"
    ></div>

    <div class="relative z-10 flex items-center justify-between">
      <div class="flex items-center gap-2">
        <div
          class="flex h-8 w-8 items-center justify-center rounded-full bg-white/30 text-white"
        >
          <i class="fa-solid fa-star text-brand-gold/50"></i>
        </div>
        <span class="text-sm font-medium text-slate-600"
          >Currently Net Worth</span
        >
      </div>
    </div>

    <div class="mt-4">
      <h2 class="text-5xl font-extrabold tracking-tight text-slate-800">
        $ {{ amount }}
      </h2>
    </div>
  </div>
</template>
