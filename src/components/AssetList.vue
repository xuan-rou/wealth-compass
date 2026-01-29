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
      class="flex items-center justify-between rounded-2xl bg-white/30 p-4 backdrop-blur-sm border border-white/40"
    >
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
