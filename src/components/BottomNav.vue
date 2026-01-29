<script setup lang="ts">
defineProps<{
  activeTab?: string
}>()

const tabs = [
  {
    name: 'Assets',
    icon: 'fa-sack-dollar',
    id: 'assets',
  },
  { name: 'Charts', icon: 'fa-chart-area', id: 'charts' },
  { name: 'Add', icon: 'fa-plus', id: 'add', isFloating: true },
  { name: 'Goals', icon: 'fa-bullseye', id: 'goals' },
  { name: 'Settings', icon: 'fa-gear', id: 'settings' },
]
</script>

<template>
  <nav
    class="fixed right-0 bottom-0 left-0 z-50 rounded-t-4xl border-t border-white/50 bg-white/90 px-6 py-4 shadow-[0_-5px_30px_-5px_rgba(0,0,0,0.1)] backdrop-blur-xl"
  >
    <div class="mx-auto flex max-w-md items-center justify-between">
      <template v-for="tab in tabs" :key="tab.id">
        <!-- Floating Action Button -->
        <button
          v-if="tab.isFloating"
          class="-mt-12 flex h-16 w-16 items-center justify-center rounded-full border-4 border-white bg-indigo-600 text-white shadow-lg transition-transform active:scale-95"
        >
          <i class="fa-solid text-2xl" :class="tab.icon"></i>
        </button>

        <!-- Regular Tab -->
        <button
          v-else
          :class="[
            'flex flex-col items-center gap-1 transition-colors',
            activeTab === tab.id
              ? 'text-indigo-600'
              : 'text-slate-400 hover:text-indigo-400',
          ]"
        >
          <i class="fa-solid text-2xl" :class="tab.icon"></i>
          <span
            :class="[
              'text-xs',
              activeTab === tab.id ? 'font-bold' : 'font-medium',
            ]"
            >{{ tab.name }}</span
          >
        </button>
      </template>
    </div>
  </nav>
</template>
