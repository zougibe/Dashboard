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
      <RecipesTable :titles="titles" :recipes="recipes" />
    </div>
  </div>
</template>

<script setup>
import RecipesTable from "../../components/RecipesTable";

const titles = [
  {
    val1: "Recipe Name",
    val2: "Duration",
    val3: "Ingredients",
    val4: "Video",
    val5: "Image",
    val6: "Rate",
    val7: "Actions",
  },
];

const recipes = [
  {
    recipeName: "Rice",
    duration: "45min",
    ingredient: "Rice,water",
    video: "Link",
    image: "Link",
    rate: "5.4",
  },
  {
    recipeName: "Rice",
    duration: "45min",
    ingredient: "Rice,water",
    video: "Link",
    image: "Link",
    rate: "5.4",
  },
  {
    recipeName: "Rice",
    duration: "45min",
    ingredient: "Rice,water",
    video: "Link",
    image: "Link",
    rate: "5.4",
  },
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
