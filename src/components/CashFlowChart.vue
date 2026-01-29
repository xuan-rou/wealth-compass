<script setup lang="ts">
// Mock data for the chart bars
const bars = [
  { h: '40%', color: 'bg-indigo-300' },
  { h: '60%', color: 'bg-purple-300' },
  { h: '30%', color: 'bg-blue-300' },
  { h: '80%', color: 'bg-indigo-400' },
  { h: '50%', color: 'bg-purple-400' },
  { h: '70%', color: 'bg-blue-400' },
  { h: '45%', color: 'bg-indigo-300' },
  { h: '65%', color: 'bg-purple-300' },
]
</script>

<template>
  <div class="flex h-full w-full items-end justify-between gap-2 px-2 pt-4">
    <div 
      v-for="(bar, index) in bars" 
      :key="index"
      :class="['w-full rounded-t-lg opacity-80 backdrop-blur-sm transition-all hover:opacity-100', bar.color]"
      :style="{ height: bar.h }"
    ></div>
  </div>
</template>
