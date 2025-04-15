<template>
  <div class="overflow-x-auto">
    <table class="min-w-full text-sm text-left text-gray-700">
      <thead class="bg-gray-100 text-xs uppercase">
        <tr v-for="(title, index) in titles" :key="index">
          <th scope="col" class="px-6 py-3">{{ title.val1 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val2 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val3 }}</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(category, index) in categories"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50"
        >
          <td class="px-6 py-4 whitespace-nowrap">
            {{ category.categoryName }}
          </td>
          <td class="px-6 py-4 whitespace-nowrap">{{ category.image }}</td>
          <td class="px-6 py-4 whitespace-nowrap">
            <div class="flex gap-2">
              <button
                class="bg-green-500 text-white px-4 py-2 rounded-md hover:bg-green-600 transition-colors"
              >
                Edit
              </button>
              <button
                class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600 transition-colors"
              >
                Delete
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const props = defineProps({
  categories: {
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
