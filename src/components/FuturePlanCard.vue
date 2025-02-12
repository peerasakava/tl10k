<script setup>
defineProps({
  headline: {
    type: String,
    required: true
  },
  summary: {
    type: String,
    required: true
  },
  managementQuote: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div class="bg-blue-100/50 rounded-lg p-6 border border-blue-200 hover:shadow-lg transition-shadow">
    <h3 class="text-xl font-semibold text-gray-700 mb-4">{{ headline }}</h3>
    
    <blockquote v-if="managementQuote" class="mb-4 pl-4 border-l-4 border-blue-500 bg-blue-50 p-4 rounded-r-lg italic">
      <p class="text-gray-700 font-medium">"{{ managementQuote }}"</p>
    </blockquote>

    <p class="text-gray-600">{{ summary }}</p>
  </div>
</template>
