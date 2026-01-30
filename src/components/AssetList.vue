<script setup lang="ts">
interface AssetItem {
  name: string
  amount: string
  icon: string
  color: string
}

defineProps<{
  items: AssetItem[]
}>()
</script>

<template>
  <div class="flex flex-col gap-3">
    <div 
      v-for="(item, index) in items" 
      :key="index"
      class="relative flex items-center justify-between overflow-hidden rounded-2xl border border-white/60 bg-linear-to-br from-white/50 via-white/30 to-white/20 p-4 shadow-xl backdrop-blur-xl"
      style="box-shadow: 0 4px 24px 0 rgba(99, 102, 241, 0.1), inset 0 1px 0 0 rgba(255, 255, 255, 0.5);"
    >
      <!-- Glossy highlight overlay -->
      <div
        class="pointer-events-none absolute inset-0 bg-linear-to-br from-white/30 via-transparent to-transparent opacity-50"
        style="mask-image: radial-gradient(circle at top left, black 20%, transparent 65%);"
      ></div>
      
      <!-- Liquid flow effect -->
      <div
        class="pointer-events-none absolute -top-6 -right-6 h-24 w-24 rounded-full bg-linear-to-br from-indigo-200/15 via-purple-200/10 to-transparent blur-xl"
      ></div>
      <div class="flex items-center gap-4">
        <div :class="['flex h-12 w-12 items-center justify-center rounded-full text-2xl shadow-sm', item.color]">
          {{ item.icon }}
        </div>
        <span class="text-lg font-bold text-slate-700">{{ item.name }}</span>
      </div>
      
      <div class="flex items-center gap-3">
        <span class="text-lg font-bold text-slate-800">$ {{ item.amount }}</span>
        <div class="flex h-8 w-8 items-center justify-center rounded-full bg-white/50 text-slate-400">
            <span class="text-xs">➜</span>
        </div>
      </div>
    </div>
  </div>
</template>
