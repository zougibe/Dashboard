<template>
  <div class="p-4">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold">Recipes</h2>
      <button
        class="px-4 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
      >
        Add Recipe
      </button>
    </div>

    <div class="bg-white rounded-lg shadow overflow-hidden">
      <RecipesTable :titles="titles" :users="users" />
    </div>
  </div>
</template>

<script setup>
import UsersTable from "../../components/UsersTable";

const titles = [
  {
    val1: "Customer Name",
    val2: "Orders",
    val3: "Favorites",
    val4: "Image",
    val5: "Rate",
    val6: "Actions",
  },
];

const users = [
  {
    recipeName: "Rice",
    duration: "45min",
    ingredient: "Rice,water",
    video: "Link",
    image: "Link",
    rate: "5.4",
  },
];

definePageMeta({
  layout: "admin",
});
</script>
