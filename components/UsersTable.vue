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
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(user, index) in users"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50"
        >
          <td class="px-6 py-4 whitespace-nowrap">{{ user.x }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ user.x }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ user.x }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ user.x }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ user.x }}</td>
          <td class="px-6 py-4 whitespace-nowrap">{{ user.x }}</td>
          <td class="px-6 py-4 whitespace-nowrap">
            <div class="flex gap-2">
              <button
                class="bg-green-500 text-orange-50 px-4 py-2 rounded-md cursor-pointer"
              >
                Edit
              </button>
              <button
                class="bg-red-500 text-orange-50 px-4 py-2 rounded-md cursor-pointer"
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
  users: {
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
