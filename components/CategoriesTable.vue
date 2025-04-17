<template>
  <div class="overflow-x-auto">
    <table class="min-w-full text-sm text-left text-gray-700">
      <thead class="bg-gray-100 text-xs uppercase">
        <tr>
          <th class="px-6 py-3">Category Name</th>
          <th class="px-6 py-3">Image</th>
          <th class="px-6 py-3">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(category, index) in categories"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50"
        >
          <td class="px-6 py-4 whitespace-nowrap">{{ category.categoryName }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ category.image }}</td>
          <td class="px-6 py-4 whitespace-nowrap">
            <div class="flex gap-2">
              <button
                @click="$emit('edit-category', index)"
                class="bg-green-500 text-white px-4 py-2 rounded-md hover:bg-green-600 transition"
              >
                Edit
              </button>
              <button
                @click="$emit('delete-category', index)"
                class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600 transition"
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
defineProps({
  categories: {
    type: Array,
    required: true,
    default: () => [],
  },
});
</script>
