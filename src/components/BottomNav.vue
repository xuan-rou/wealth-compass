<script setup lang="ts">
import { ref } from 'vue'

// 定義 Tab 的型別
interface Tab {
  name: string
  icon: string
  id: string
  isFloating?: boolean
}

// 定義 SubItem 的型別
interface SubItem {
  text: string
  class: string
}

defineProps<{
  activeTab?: string
}>()

const emit = defineEmits<{
  openAddAsset: []
}>()

const isOpenAddBtn = ref<boolean>(false)

const tabs: Tab[] = [
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

const subItems: SubItem[] = [
  { text: 'Assets', class: 'bg-mint-green/50 top-5' },
  { text: 'Debt', class: 'bg-sky-blue/50' },
  { text: 'Income', class: 'bg-lavender/50 top-5' },
]

const handleSubItemClick = (index: number) => {
  if (index === 0) {
    // Assets button
    emit('openAddAsset')
    isOpenAddBtn.value = false
  }
  // TODO: Handle other sub-items (Debt, Income)
}
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
          @click="isOpenAddBtn = !isOpenAddBtn"
          class="bg-primary-dark -mt-12 flex h-16 w-16 items-center justify-center rounded-full border-4 border-white text-white shadow-lg transition-transform active:scale-95"
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

        <!-- Floating Action Sub Button -->
        <div
          v-show="isOpenAddBtn"
          class="absolute bottom-28 left-1/2 flex -translate-x-1/2 gap-x-3"
        >
          <button
            v-for="(item, index) in subItems"
            :key="index"
            @click="handleSubItemClick(index)"
            class="animate-bounce-in relative flex h-16 w-16 items-center justify-center rounded-full border-3 border-white text-white drop-shadow-md drop-shadow-violet-200/20"
            :class="item.class"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            {{ item.text }}
          </button>
        </div>
      </template>
    </div>
  </nav>
</template>

<style scoped>
@keyframes droplet-separate {
  0% {
    opacity: 0;
    transform: scale(0) translateY(100px);
  }
  50% {
    opacity: 0.5;
    transform: scaleX(1.05);
  }
  100% {
    opacity: 1;
    transform: scaleX(1) translateY(0);
  }
}

.animate-bounce-in {
  animation: droplet-separate 1s cubic-bezier(0.25, 1, 0.5, 1) forwards;
  opacity: 0;
}
</style>
