<script setup>
defineProps({
  name: {
    type: String,
    required: true
  },
  summary: {
    type: String,
    required: true
  },
  details: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="bg-purple-100/50 rounded-lg p-6 border border-purple-200 hover:shadow-lg transition-shadow">
    <h3 class="text-xl font-semibold text-gray-700 mb-2">{{ name }}</h3>
    <p class="text-gray-600 mb-2"><span class="font-medium">Summary:</span> {{ summary }}</p>
    <p class="text-gray-600"><span class="font-medium">Details:</span> {{ details }}</p>
  </div>
</template>
