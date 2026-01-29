<script setup lang="ts"></script>

<template>
  <div
    class="bg-card-bg shadow-dreamy rounded-3xl border border-white/40 p-5 backdrop-blur-sm"
  >
    <p class="mb-2 text-sm text-slate-500">
      <slot name="title"></slot>
    </p>
    <p class="text-primary-dark text-2xl font-bold">
      $ <slot name="amount"></slot>
    </p>
  </div>
</template>

<style scoped></style>
