<template>
  <div class="bg-white rounded-lg shadow-md p-6 h-full">
    <h3 class="text-xl font-semibold mb-4">{{ tableTitle }}</h3>
    <div class="overflow-x-auto">
      <table class="w-full table-auto">
        <thead>
          <tr class="bg-gray-50">
            <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Category</th>
            <th class="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">Amount (MUSD)</th>
          </tr>
        </thead>
        <tbody class="bg-white divide-y divide-gray-200">
          <tr v-for="item in items" :key="item.title">
            <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">{{ item.title }}</td>
            <td class="px-6 py-4 whitespace-nowrap text-sm text-right text-gray-900">
              {{ formatAmount(item.amount) }}
            </td>
          </tr>
          <tr class="bg-gray-50 font-semibold">
            <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">Total</td>
            <td class="px-6 py-4 whitespace-nowrap text-sm text-right text-gray-900">
              {{ formatAmount(totalAmount) }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  tableTitle: {
    type: String,
    required: true
  },
  items: {
    type: Array,
    required: true
  }
})

const totalAmount = computed(() => {
  return props.items.reduce((sum, item) => sum + item.amount, 0)
})

const formatAmount = (amount) => {
  // Format as millions if amount is over 1 million
  if (amount >= 1000000) {
    return `$${(amount / 1000000).toFixed(2)}M`
  }
  // Format as thousands if amount is over 1 thousand
  if (amount >= 1000) {
    return `$${(amount / 1000).toFixed(2)}K`
  }
  // Otherwise format as regular number
  return `$${amount.toFixed(2)}`
}
</script>
