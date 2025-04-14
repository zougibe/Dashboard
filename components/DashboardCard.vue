<template>
  <div class="bg-white rounded-2xl shadow-md p-6">
    <h3 class="text-gray-800 font-bold text-[20px] mb-2">{{ title }}</h3>
    <div class="text-3xl font-bold text-orange-500">{{ value }}</div>
    <div class="text-sm text-gray-600 mt-1">{{ unit }}</div>
  </div>
</template>

<script setup>
const props = defineProps({
  title: { type: String, required: true },
  value: { type: String, required: true },
  unit: { type: String, default: "" },
});
</script>
