<script setup>
defineProps({
  description: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="bg-emerald-50 rounded-lg shadow-md p-6 xl:col-span-3">
    <h3 class="text-xl font-semibold text-gray-700 mb-2">📋 Business Description</h3>
    <p class="text-gray-600">{{ description }}</p>
  </div>
</template>
