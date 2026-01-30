<script setup lang="ts">
defineProps<{
  title?: string
  amount?: string
  icon?: string
}>()
</script>

<template>
  <div
    class="relative flex h-full flex-col overflow-hidden rounded-4xl border border-white/60 bg-linear-to-br from-white/50 via-white/30 to-white/20 p-5 shadow-2xl backdrop-blur-xl"
    style="
      box-shadow:
        0 8px 32px 0 rgba(99, 102, 241, 0.12),
        inset 0 1px 0 0 rgba(255, 255, 255, 0.5);
    "
  >
    <!-- Glossy highlight overlay -->
    <div
      class="pointer-events-none absolute inset-0 bg-linear-to-br from-white/40 via-transparent to-transparent opacity-50"
      style="
        mask-image: radial-gradient(
          circle at top left,
          black 15%,
          transparent 60%
        );
      "
    ></div>

    <!-- Liquid flow effect -->
    <div
      class="pointer-events-none absolute -top-10 -right-10 h-40 w-40 rounded-full bg-linear-to-br from-indigo-200/20 via-purple-200/10 to-transparent blur-2xl"
    ></div>
    <div v-if="title" class="mb-2 flex items-center gap-2">
      <div
        class="flex h-8 w-8 shrink-0 items-center justify-center rounded-full bg-white/70 text-lg shadow-xs"
      >
        <i v-if="icon" :class="icon"></i>
      </div>
      <span class="text-sm font-semibold text-slate-500">{{ title }}</span>
    </div>

    <div class="flex flex-1 flex-col justify-center">
      <slot>
        <p v-if="amount" class="text-2xl font-bold text-slate-800">
          $ {{ amount }}
        </p>
      </slot>
    </div>
  </div>
</template>
