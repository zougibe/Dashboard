<template>
  <div class="p-4">
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold">Chefs</h2>
      <button
        class="px-4 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
      >
        Add Chef
      </button>
    </div>

    <div class="bg-white rounded-lg shadow overflow-hidden">
      <ChefsTable :titles="titles" :chefs="chefs" />
    </div>
  </div>
</template>

<script setup>
import ChefsTable from "../../components/ChefsTable";

const titles = [
  {
    val1: "Chef Name",
    val2: "Title",
    val3: "Bio",
    val4: "No.Recipes",
    val5: "No.Orders",
    val6: "Rate",
    val7: "Image",
    val8: "Actions",
  },
];

const chefs = [
  {
    ChefName: "Ahmed",
    recipeName: "Fried Rice",
    bio: "25 year old",
    totalR: "65",
    totalO: "123",
    rate: "4.9",
    image: "link",
  },
  {
    ChefName: "Ahmed",
    recipeName: "Fried Rice",
    bio: "25 year old",
    totalR: "65",
    totalO: "123",
    rate: "4.9",
    image: "link",
  },
  {
    ChefName: "Ahmed",
    recipeName: "Fried Rice",
    bio: "25 year old",
    totalR: "65",
    totalO: "123",
    rate: "4.9",
    image: "link",
  },
];

definePageMeta({
  layout: "admin",
});
</script>
