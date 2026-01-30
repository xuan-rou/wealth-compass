<script setup lang="ts">
defineProps<{
  amount: string
}>()
</script>

<template>
  <div
    class="relative overflow-hidden rounded-4xl border border-white/60 bg-linear-to-br from-white/50 via-white/30 to-white/20 p-6 shadow-2xl backdrop-blur-xl"
    style="
      box-shadow:
        0 8px 32px 0 rgba(99, 102, 241, 0.15),
        inset 0 1px 0 0 rgba(255, 255, 255, 0.6);
    "
  >
    <!-- Glossy highlight overlay -->
    <div
      class="absolute inset-0 bg-linear-to-br from-white/40 via-transparent to-transparent opacity-60"
      style="
        mask-image: radial-gradient(
          circle at top left,
          black 20%,
          transparent 70%
        );
      "
    ></div>

    <!-- Liquid flow effect -->
    <div
      class="absolute -top-20 -right-20 h-60 w-60 rounded-full bg-linear-to-br from-indigo-200/30 via-purple-200/20 to-transparent blur-3xl"
    ></div>

    <div class="relative z-10 flex items-center justify-between">
      <div class="flex items-center gap-2">
        <div
          class="flex h-8 w-8 items-center justify-center rounded-full bg-white/70 text-white shadow-xs"
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
