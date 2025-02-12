<script setup>
defineProps({
  title: {
    type: String,
    required: true
  },
  content: {
    type: String,
    required: true
  },
  icon: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="bg-emerald-100/50 rounded-lg p-6 border border-emerald-200 hover:shadow-lg transition-shadow">
    <h3 class="text-lg font-semibold text-gray-700 mb-2">{{ icon }} {{ title }}</h3>
    <p class="text-gray-600">{{ content }}</p>
  </div>
</template>
