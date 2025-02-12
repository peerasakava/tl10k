<script setup>
defineProps({
  title: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="mb-12">
    <h2 class="text-2xl font-bold text-gray-800 mb-6 pb-2 border-b-2 border-gray-200">{{ title }}</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
      <slot></slot>
    </div>
  </div>
</template>
