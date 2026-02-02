<script setup lang="ts">
import { ref } from 'vue'
import NetWorthCard from './components/NetWorthCard.vue'
import StatCard from './components/StatCard.vue'
import AssetList from './components/AssetList.vue'
import BottomNav from './components/BottomNav.vue'
import CashFlowChart from './components/CashFlowChart.vue'

// Import the generated mascot (assuming it's placed in assets or handled via public)
// For this demo, we'll assume the user will move the file or we reference it if in public.
// Since we can't easily move the generated file to public/assets without command, we will use a placeholder or check if we can copy it.
// I'll assume we can use the relative path if I move it. For now, I'll use a placeholder text if image missing.

const assetItems = ref([
  {
    name: 'Cash',
    amount: '150',
    icon: '💵',
    color: 'bg-green-100/50 text-green-600',
  },
  {
    name: 'Jade',
    amount: '5',
    icon: '💎',
    color: 'bg-teal-100/50 text-teal-600',
  },
])
</script>

<template>
  <div
    class="min-h-screen overflow-x-hidden bg-[url(./assets/img/bg.png)] bg-contain bg-no-repeat pt-12 text-slate-700 selection:bg-indigo-100"
  >
    <header class="mb-8 flex items-center justify-between px-6">
      <!-- Menu Icon -->
      <div class="cursor-pointer">
        <i class="fa-solid fa-bars text-3xl text-white"></i>
      </div>

      <div
        class="h-10 w-10 overflow-hidden rounded-full border-2 border-white bg-indigo-100 shadow-sm"
      >
        <img
          src="https://api.dicebear.com/7.x/avataaars/svg?seed=Felix"
          alt="User"
        />
      </div>
    </header>

    <main
      class="absolute bottom-0 flex h-[calc(100vh-220px)] w-full flex-col gap-6 overflow-y-auto rounded-t-[2.85rem] bg-(image:--image-dreamy-gradient) px-6 pt-6 pb-28 drop-shadow-lg"
    >
      <!-- Hero Section -->
      <section>
        <NetWorthCard amount="1,100,000" />
      </section>

      <!-- Stats Grid -->
      <section class="grid grid-cols-2 gap-4">
        <div class="flex flex-col gap-4">
          <StatCard
            title="Total Assets"
            amount="1,100,000"
            :icon="'fa-solid fa-sack-dollar text-blue-600/40'"
          />
          <StatCard
            title="Total Liabilities"
            amount="100,000"
            :icon="'fa-solid fa-cash-register text-blue-600/40'"
          />
        </div>
        <div class="h-full">
          <StatCard
            title="Asset Allocation"
            :icon="'fa-solid fa-chart-pie text-blue-600/40'"
          >
            <!-- Simple CSS Donut Chart Mock -->
            <div class="relative mx-auto mt-2 h-32 w-32">
              <div
                class="absolute inset-0 rounded-full border-12 border-indigo-300"
              ></div>
              <div
                class="absolute inset-0 rotate-45 rounded-full border-12 border-transparent border-t-purple-400"
              ></div>
              <div
                class="absolute inset-0 rotate-[120deg] rounded-full border-[12px] border-transparent border-l-teal-300"
              ></div>
              <div
                class="absolute inset-4 flex items-center justify-center rounded-full bg-white/50 backdrop-blur-sm"
              >
                <span class="text-xs font-bold text-slate-500">MIX</span>
              </div>
            </div>
          </StatCard>
        </div>
      </section>

      <!-- Monthly Cashflow -->
      <section>
        <StatCard
          title="Monthly Cashflow"
          :icon="'fa-solid fa-chart-line text-blue-600/40'"
        >
          <CashFlowChart />
        </StatCard>
      </section>

      <!-- Asset List -->
      <section>
        <div class="mb-4 flex items-center justify-between px-2">
          <h3 class="text-lg font-bold text-slate-800">Asset List</h3>
          <button class="text-sm font-bold text-indigo-600">View All</button>
        </div>
        <AssetList :items="assetItems" />
      </section>
    </main>

    <BottomNav activeTab="assets" />
  </div>
</template>

<style>
/* Global scrollbar hide for cleaner UI */
::-webkit-scrollbar {
  display: none;
}
</style>
