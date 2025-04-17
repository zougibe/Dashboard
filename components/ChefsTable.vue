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
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(chef, index) in chefs"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50"
        >
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.ChefName }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.recipeName }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.bio }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.totalR }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.totalO }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.rate }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ chef.image }}</td>
          <td class="px-6 py-4 whitespace-nowrap">
            <div class="flex gap-2">
              <button
                @click="$emit('edit-chef', index)"
                class="bg-green-500 text-white px-4 py-2 rounded-md cursor-pointer hover:bg-green-600 transition"
              >
                Edit
              </button>
              <button
                @click="$emit('delete-chef', index)"
                class="bg-red-500 text-white px-4 py-2 rounded-md cursor-pointer hover:bg-red-600 transition"
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
  chefs: {
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

defineEmits(["edit-chef", "delete-chef"]);
</script>
