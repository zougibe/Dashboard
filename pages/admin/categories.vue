<template>
  <div class="p-4">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold">Categories</h2>
      <button
        class="px-4 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
      >
        Add Category
      </button>
    </div>

    <div class="bg-white rounded-lg shadow overflow-hidden">
      <CategoriesTable :titles="titles" :categories="categories" />
    </div>
  </div>
</template>

<script setup>
import CategoriesTable from "../../components/CategoriesTable";

const titles = [
  {
    val1: "Category Name",
    val2: "Image",
    val3: "Action",
  },
];

const categories = [
  {
    categoryName: "FastFood",
    image: "link",
  },
  {
    categoryName: "Asian",
    image: "link",
  },
  {
    categoryName: "Healthy",
    image: "link",
  },
];

definePageMeta({
  layout: "admin",
});
</script>
