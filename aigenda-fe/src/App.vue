<script setup lang="ts">
import CountdownTimer from './components/CountdownTimer.vue'
</script>

<template>

  <h2 class="text-center text-xl sm:text-2xl font-medium text-gray-700 mb-4">AIgenda</h2>
  
  <div class="min-h-screen bg-gray-100 flex flex-col items-center justify-center p-4 sm:p-6">
    <div class="w-full max-w-md lg:max-w-lg">
      <CountdownTimer />
    </div>
  </div>
</template>

<style scoped></style>
