<script setup lang="ts">
defineProps<{
  title?: string
  amount?: string
  icon?: string
  iconColor?: string
}>()
</script>

<template>
  <div
    class="flex h-full flex-col rounded-4xl border border-white/50 bg-white/40 p-5 shadow-sm backdrop-blur-md"
  >
    <div v-if="title" class="mb-2 flex items-center gap-2">
      <div
        class="flex h-8 w-8 items-center justify-center rounded-full text-lg"
      >
        <i v-if="icon" :class="(icon, iconColor)"></i>
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
