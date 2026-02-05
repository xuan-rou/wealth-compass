<script setup lang="ts">
import { ref } from 'vue'

interface AssetType {
  id: string
  name: string
  icon: string
  color: string
}

const assetTypes: AssetType[] = [
  {
    id: 'cash',
    name: 'Cash',
    icon: '💵',
    color: 'bg-green-100/50 text-green-600',
  },
  {
    id: 'stocks',
    name: 'Stocks',
    icon: '📈',
    color: 'bg-blue-100/50 text-blue-600',
  },
  {
    id: 'crypto',
    name: 'Cryptocurrency',
    icon: '₿',
    color: 'bg-orange-100/50 text-orange-600',
  },
  {
    id: 'real-estate',
    name: 'Real Estate',
    icon: '🏠',
    color: 'bg-purple-100/50 text-purple-600',
  },
  {
    id: 'precious-metals',
    name: 'Precious Metals',
    icon: '💎',
    color: 'bg-teal-100/50 text-teal-600',
  },
  {
    id: 'other',
    name: 'Other',
    icon: '📦',
    color: 'bg-gray-100/50 text-gray-600',
  },
]

const selectedAssetType = ref<string>('')
const amount = ref<string>('')
const isDropdownOpen = ref<boolean>(false)

const emit = defineEmits<{
  close: []
  submit: [{ type: string; amount: string }]
}>()

const selectAssetType = (type: AssetType) => {
  selectedAssetType.value = type.id
  isDropdownOpen.value = false
}

const getSelectedAssetType = (): AssetType | undefined => {
  return assetTypes.find((type) => type.id === selectedAssetType.value)
}

const handleSubmit = () => {
  if (!selectedAssetType.value || !amount.value) {
    return
  }

  emit('submit', {
    type: selectedAssetType.value,
    amount: amount.value,
  })

  // Reset form
  selectedAssetType.value = ''
  amount.value = ''
}

const handleClose = () => {
  emit('close')
}
</script>

<template>
  <div
    class="fixed inset-0 z-50 flex items-end justify-center bg-black/40 backdrop-blur-sm"
    @click.self="handleClose"
  >
    <div
      class="w-full max-w-md animate-slide-up rounded-t-4xl border-t border-white/60 bg-linear-to-br from-white/95 via-white/90 to-white/85 p-6 pb-8 shadow-2xl backdrop-blur-xl"
    >
      <!-- Header -->
      <div class="mb-6 flex items-center justify-between">
        <h2 class="text-2xl font-bold text-slate-800">Add New Asset</h2>
        <button
          @click="handleClose"
          class="flex h-8 w-8 items-center justify-center rounded-full bg-slate-100/80 text-slate-600 transition-colors hover:bg-slate-200/80"
        >
          <i class="fa-solid fa-xmark text-lg"></i>
        </button>
      </div>

      <!-- Form -->
      <form @submit.prevent="handleSubmit" class="space-y-5">
        <!-- Asset Type Dropdown -->
        <div class="relative">
          <label class="mb-2 block text-sm font-semibold text-slate-600">
            Asset Type
          </label>
          <button
            type="button"
            @click="isDropdownOpen = !isDropdownOpen"
            class="flex w-full items-center justify-between rounded-2xl border border-white/60 bg-white/70 px-4 py-3.5 text-left shadow-lg backdrop-blur-sm transition-all hover:bg-white/90 focus:outline-none focus:ring-2 focus:ring-indigo-400/50"
          >
            <div v-if="selectedAssetType" class="flex items-center gap-3">
              <span class="text-2xl">{{
                getSelectedAssetType()?.icon
              }}</span>
              <span class="font-medium text-slate-800">{{
                getSelectedAssetType()?.name
              }}</span>
            </div>
            <span v-else class="text-slate-400">Select asset type</span>
            <i
              class="fa-solid fa-chevron-down text-slate-400 transition-transform"
              :class="{ 'rotate-180': isDropdownOpen }"
            ></i>
          </button>

          <!-- Dropdown Menu -->
          <div
            v-show="isDropdownOpen"
            class="absolute z-10 mt-2 max-h-64 w-full overflow-y-auto rounded-2xl border border-white/60 bg-white/95 shadow-2xl backdrop-blur-xl"
          >
            <button
              v-for="type in assetTypes"
              :key="type.id"
              type="button"
              @click="selectAssetType(type)"
              class="flex w-full items-center gap-3 border-b border-slate-100/50 px-4 py-3 text-left transition-colors last:border-b-0 hover:bg-indigo-50/50"
            >
              <span class="text-2xl">{{ type.icon }}</span>
              <span class="font-medium text-slate-800">{{ type.name }}</span>
            </button>
          </div>
        </div>

        <!-- Amount Input -->
        <div>
          <label class="mb-2 block text-sm font-semibold text-slate-600">
            Amount
          </label>
          <div
            class="flex items-center gap-2 rounded-2xl border border-white/60 bg-white/70 px-4 py-3.5 shadow-lg backdrop-blur-sm transition-all focus-within:bg-white/90 focus-within:ring-2 focus-within:ring-indigo-400/50"
          >
            <span class="text-xl font-bold text-slate-600">$</span>
            <input
              v-model="amount"
              type="number"
              step="0.01"
              placeholder="0.00"
              class="w-full bg-transparent text-lg font-medium text-slate-800 placeholder-slate-400 focus:outline-none"
            />
          </div>
        </div>

        <!-- Action Buttons -->
        <div class="flex gap-3 pt-4">
          <button
            type="button"
            @click="handleClose"
            class="flex-1 rounded-2xl border border-slate-200 bg-slate-100/80 px-6 py-3.5 font-semibold text-slate-700 shadow-md transition-all hover:bg-slate-200/80 active:scale-95"
          >
            Cancel
          </button>
          <button
            type="submit"
            :disabled="!selectedAssetType || !amount"
            class="bg-primary-dark flex-1 rounded-2xl px-6 py-3.5 font-semibold text-white shadow-lg transition-all hover:shadow-xl active:scale-95 disabled:cursor-not-allowed disabled:opacity-50"
          >
            Add Asset
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
@keyframes slide-up {
  from {
    transform: translateY(100%);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.animate-slide-up {
  animation: slide-up 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

/* Custom scrollbar for dropdown */
::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: rgba(148, 163, 184, 0.3);
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgba(148, 163, 184, 0.5);
}
</style>
