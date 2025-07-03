<script setup lang="ts">

defineProps<{ msg: string }>()

</script>
<template>
  <h1 class="text-2xl font-bold bg-green-500">{{ msg }}</h1>
</template>
