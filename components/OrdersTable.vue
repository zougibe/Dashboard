<template>
  <div class="overflow-x-auto">
    <table class="min-w-full text-sm text-left text-gray-700">
      <thead class="bg-gray-100 text-xs uppercase">
        <tr v-for="(title, index) in titles" :key="index">
          <th scope="col" class="px-6 py-3">{{ title.val1 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val2 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val3 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val4 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val5 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val6 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val7 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val8 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val9 }}</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(order, index) in orders"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50"
        >
          <td class="px-6 py-4 whitespace-nowrap">{{ order.customerName }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ order.recipeName }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ order.paymentMethod }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ order.total }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ order.address }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ order.phone }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ order.notes }}</td>
          <td class="px-6 py-4 whitespace-nowrap text-orange-500">
            {{ order.status }}
          </td>
          <td class="px-6 py-4 whitespace-nowrap text-orange-500">
            <button
              class="bg-orange-500 text-orange-50 px-4 py-2 rounded-md cursor-pointer"
            >
              Mark as Done
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const props = defineProps({
  orders: {
    type: Array,
    required: true,
    default: () => [],
  },
  titles: {
    type: Array,
    required: true,
    default: () => [],
  },
});
</script>
