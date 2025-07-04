<template>
  <button @click="playSound" class="px-4 py-2 bg-blue-500 text-white rounded shadow hover:bg-blue-600 transition">
    Ding
  </button>
</template>

<script setup lang="ts">
const playSound = () => {

  const audio = new Audio(import.meta.env.BASE_URL + 'doorbell.mp3');
  audio.play().catch((err) => {
    console.error('Audio could not be played:', err);
  });
};
</script>

<style scoped>
button {
  font-size: 1.2rem;
  font-weight: 600;
}
</style>
