<template>
  <div class="rounded-lg bg-white shadow-lg p-4 sm:p-6 w-full">

    <!-- Timer Display -->
    <div class="text-center mb-6">
      <div class="text-6xl sm:text-7xl font-bold tracking-tighter">
        {{ formattedTime }}
      </div>
      <div v-if="isRunning" class="mt-2 text-sm text-gray-500">
        Timer läuft...
      </div>
    </div>

    <!-- Time Settings (visible only when timer is not running) -->
    <div v-if="!isRunning" class="mb-4">
      <div class="flex items-center justify-center gap-4 mb-2">
        <button @click="decreaseTime(60)" class="p-1 px-2 bg-gray-200 rounded hover:bg-gray-300 text-lg">-</button>
        <span class="text-sm font-medium">{{ Math.floor(time / 60) }} min</span>
        <button @click="increaseTime(60)" class="p-1 px-2 bg-gray-200 rounded hover:bg-gray-300 text-lg">+</button>
      </div>
      <div class="flex items-center justify-center gap-2">
        <button @click="time = 300"
          class="px-2 py-1 text-xs bg-blue-100 text-blue-800 rounded hover:bg-blue-200">5min</button>
        <button @click="time = 600"
          class="px-2 py-1 text-xs bg-blue-100 text-blue-800 rounded hover:bg-blue-200">10min</button>
        <button @click="time = 900"
          class="px-2 py-1 text-xs bg-blue-100 text-blue-800 rounded hover:bg-blue-200">15min</button>
        <button @click="time = 1200"
          class="px-2 py-1 text-xs bg-blue-100 text-blue-800 rounded hover:bg-blue-200">20min</button>
      </div>
    </div>

    <!-- Control Buttons -->
    <div class="flex justify-between gap-2 sm:gap-4">
      <button @click="startTimer" :disabled="isRunning" :class="[
        'flex-1 py-2 rounded-md font-medium transition-colors flex items-center justify-center',
        isRunning ? 'bg-green-200 text-green-700 cursor-not-allowed' : 'bg-green-500 text-white hover:bg-green-600'
      ]">
        <svg v-if="!isRunning" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20"
          fill="currentColor">
          <path fill-rule="evenodd"
            d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z"
            clip-rule="evenodd" />
        </svg>
        <span>Start</span>
      </button>

      <button @click="stopTimer" :disabled="!isRunning" :class="[
        'flex-1 py-2 rounded-md font-medium transition-colors flex items-center justify-center',
        !isRunning ? 'bg-red-200 text-red-700 cursor-not-allowed' : 'bg-red-500 text-white hover:bg-red-600'
      ]">
        <svg v-if="isRunning" xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20"
          fill="currentColor">
          <path fill-rule="evenodd"
            d="M10 18a8 8 0 100-16 8 8 0 000 16zM8 7a1 1 0 00-1 1v4a1 1 0 001 1h4a1 1 0 001-1V8a1 1 0 00-1-1H8z"
            clip-rule="evenodd" />
        </svg>
        <span>Stop</span>
      </button>

      <button @click="resetTimer"
        class="flex-1 py-2 bg-gray-200 text-gray-700 rounded-md font-medium hover:bg-gray-300 transition-colors flex items-center justify-center">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-1" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd"
            d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z"
            clip-rule="evenodd" />
        </svg>
        <span>Reset</span>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onBeforeUnmount, onMounted } from 'vue';

// Timer state
const time = ref(1200); // 20 minutes in seconds
const isRunning = ref(false);
const originalTitle = ref('AIgenda');
let timerInterval: number | undefined;

// Restore original page title when component mounts
onMounted(() => {
  originalTitle.value = document.title;
});

// Reset document title when component is destroyed
onBeforeUnmount(() => {
  document.title = originalTitle.value;
});

// Formatted time display (MM:SS)
const formattedTime = computed(() => {
  const minutes = Math.floor(time.value / 60);
  const seconds = time.value % 60;
  return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
});

// Timer controls
function startTimer() {
  if (isRunning.value || time.value <= 0) return;

  isRunning.value = true;
  timerInterval = setInterval(() => {
    if (time.value <= 0) {
      stopTimer();
      playDoorbellSound();
      return;
    }
    time.value--;

    // Update document title with remaining time
    if (time.value % 5 === 0 || time.value < 20) {
      updateDocumentTitle();
    }
  }, 1000);
}

function playDoorbellSound() {
  try {
    const audio = new Audio(import.meta.env.BASE_URL + 'double-doorbell.mp3');
    audio.play();
  } catch (error) {
    console.error('Failed to play doorbell sound:', error);
  }
}

function updateDocumentTitle() {
  const minutes = Math.floor(time.value / 60);
  const seconds = time.value % 60;
  let title = `${minutes}:${seconds.toString().padStart(2, '0')} - AIgenda`;

  // Add visual indicator for remaining time
  if (time.value < 60) {
    title = `⚠️ ${title}`;
  }
  if (time.value < 20) {
    title = `🔥 ${title}`;
  }

  document.title = title;
}

function stopTimer() {
  isRunning.value = false;
  clearInterval(timerInterval);
  document.title = originalTitle.value;
}

function resetTimer() {
  stopTimer();
  time.value = 1200; // Reset to 20 minutes
}

// Time adjustment functions
function increaseTime(seconds: number) {
  if (!isRunning.value) {
    time.value += seconds;
  }
}

function decreaseTime(seconds: number) {
  if (!isRunning.value && time.value > seconds) {
    time.value -= seconds;
  } else if (!isRunning.value) {
    time.value = 0;
  }
}

// Clean up interval on component unmount
onBeforeUnmount(() => {
  clearInterval(timerInterval);
});
</script>