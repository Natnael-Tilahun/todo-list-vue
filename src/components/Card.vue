<script setup lang="ts">
// defineProps<{ msg: string }>();
defineProps<{ todo: string }>();
</script>

<template>
  <div
    class="bg-white flex flex-col border-2 rounded-lg shadow-sm px-5 py-3 justify-center gap-2"
  >
    <h1 class="text-lg font-medium">{{ todo }}</h1>
  </div>
</template>
