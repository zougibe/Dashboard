<template>
  <div class="p-4">
    <!-- Header and Add Button -->
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold">Recipes</h2>
      <button
        @click="showModal = true"
        class="px-4 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
      >
        Add Recipe
      </button>
    </div>

    <!-- Table Section -->
    <div class="bg-white rounded-lg shadow overflow-hidden">
      <RecipesTable
        :titles="titles"
        :recipes="paginatedRecipes"
        @delete-recipe="deleteRecipe"
      />
    </div>

    <!-- Pagination Section -->
    <div
      class="flex justify-center items-center gap-2 p-4 border-t border-gray-200"
    >
      <!-- Prev Button -->
      <button
        @click="goToPage(currentPage - 1)"
        :disabled="currentPage === 1"
        class="p-2 rounded-full hover:bg-gray-200 disabled:opacity-50"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="w-5 h-5"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 19l-7-7 7-7"
          />
        </svg>
      </button>

      <!-- Page Numbers -->
      <template v-for="page in visiblePages" :key="page">
        <button
          v-if="page !== '...'"
          @click="goToPage(page)"
          :class="[
            'px-3 py-1 rounded-full text-sm font-medium',
            currentPage === page
              ? 'bg-orange-500 text-white'
              : 'bg-gray-100 text-gray-800 hover:bg-orange-100',
          ]"
        >
          {{ page }}
        </button>
        <span v-else class="px-2 text-gray-500">...</span>
      </template>

      <!-- Next Button -->
      <button
        @click="goToPage(currentPage + 1)"
        :disabled="currentPage === totalPages"
        class="p-2 rounded-full hover:bg-gray-200 disabled:opacity-50"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="w-5 h-5"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M9 5l7 7-7 7"
          />
        </svg>
      </button>
    </div>

    <!-- Add Recipe Modal -->
    <div
      v-if="showModal"
      class="fixed inset-0 bg-opacity-50 flex items-center justify-center z-50"
    >
      <div class="bg-white rounded-xl shadow-xl p-6 w-[90%] max-w-lg relative">
        <!-- Close Button (X) -->
        <button
          @click="showModal = false"
          class="absolute top-3 right-3 text-gray-400 hover:text-gray-600 text-xl font-bold"
        >
          &times;
        </button>

        <h2 class="text-2xl font-bold text-black-500 mb-6 text-start">
          Add New Recipe
        </h2>

        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-black-700 mb-1"
              >Recipe Name</label
            >
            <input
              v-model="newRecipe.recipeName"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-black-700 mb-1"
              >Cooking Duration (Minutes)</label
            >
            <input
              v-model="newRecipe.duration"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-black-700 mb-1"
              >Category</label
            >
            <input
              v-model="newRecipe.category"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-black-700 mb-1"
              >Recipe Video Link</label
            >
            <input
              v-model="newRecipe.video"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-black-700 mb-1"
              >Recipe Image Link</label
            >
            <input
              v-model="newRecipe.image"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-black-700 mb-1"
              >Ingredients</label
            >
            <textarea
              v-model="newRecipe.ingredient"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400"
            ></textarea>
          </div>
        </div>

        <!-- Save Button -->
        <div class="mt-6">
          <button
            @click="saveRecipe"
            class="w-full bg-orange-500 hover:bg-orange-600 text-white font-medium px-4 py-2 rounded-lg transition"
          >
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import RecipesTable from "../../components/RecipesTable";

// Table headers
const titles = [
  {
    val1: "Recipe Name",
    val2: "Duration",
    val3: "Ingredients",
    val4: "Category",
    val5: "Video",
    val6: "Image",
    val7: "Rate",
    val8: "Description",
    val9: "Actions",
  },
];

// Recipe data
const recipes = ref([
  {
    recipeName: "Rice",
    duration: "45min",
    ingredient: "Rice, Water",
    category: "Healthy",
    video: "link",
    image: "link",
    rate: "5.4",
  },
  {
    recipeName: "Pasta",
    duration: "30min",
    ingredient: "Pasta, Tomato Sauce, Garlic, Basil",
    category: "Healthy",
    video: "link",
    image: "link",
    rate: "4.8",
  },
  {
    recipeName: "Salad",
    duration: "10min",
    ingredient: "Lettuce, Tomatoes, Cucumber, Olive Oil, Salt",
    category: "Healthy",
    video: "link",
    image: "link",
    rate: "4.5",
  },
  {
    recipeName: "Pizza",
    duration: "1hr",
    ingredient: "Dough, Tomato Sauce, Cheese, Pepperoni",
    category: "Healthy",
    video: "link",
    image: "link",
    rate: "4.9",
  },
  {
    recipeName: "Soup",
    duration: "60min",
    ingredient: "Chicken, Vegetables, Salt, Pepper",
    category: "Healthy",
    video: "link",
    image: "link",
    rate: "4.2",
  },
  {
    recipeName: "Burger",
    duration: "25min",
    ingredient: "Beef Patty, Bun, Lettuce, Tomato, Cheese",
    category: "Healthy",
    video: "link",
    image: "link",
    rate: "4.7",
  },
]);

// Modal state
const showModal = ref(false);

// New recipe form model
const newRecipe = ref({
  recipeName: "",
  duration: "",
  ingredient: "",
  category: "",
  video: "",
  image: "",
});

// Save new recipe and reset
const saveRecipe = () => {
  if (
    newRecipe.value.recipeName &&
    newRecipe.value.duration &&
    newRecipe.value.ingredient &&
    newRecipe.value.category &&
    newRecipe.value.video &&
    newRecipe.value.image
  ) {
    recipes.value.push({
      ...newRecipe.value,
      rate: "0", // default
    });

    newRecipe.value = {
      recipeName: "",
      duration: "",
      ingredient: "",
      category: "",
      video: "",
      image: "",
    };
    showModal.value = false;
    updatePaginationAfterAdd();
  }
};

// Delete recipe handler
const deleteRecipe = (paginatedIndex) => {
  const actualIndex = (currentPage.value - 1) * recipesPerPage + paginatedIndex;
  recipes.value.splice(actualIndex, 1);
  // Adjust currentPage if the current page is empty
  if (paginatedRecipes.value.length === 0 && currentPage.value > 1) {
    currentPage.value--;
  }
};

// Pagination logic
const currentPage = ref(1);
const recipesPerPage = 4;

const totalPages = computed(() =>
  Math.ceil(recipes.value.length / recipesPerPage)
);

const paginatedRecipes = computed(() => {
  const start = (currentPage.value - 1) * recipesPerPage;
  return recipes.value.slice(start, start + recipesPerPage);
});

const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

// Manage visible pages
const visiblePages = computed(() => {
  const pages = [];
  const max = totalPages.value;
  const current = currentPage.value;

  if (max <= 7) {
    for (let i = 1; i <= max; i++) pages.push(i);
  } else {
    pages.push(1);
    if (current > 4) pages.push("...");
    for (
      let i = Math.max(2, current - 2);
      i <= Math.min(max - 1, current + 2);
      i++
    ) {
      pages.push(i);
    }
    if (current < max - 3) pages.push("...");
    pages.push(max);
  }

  return pages;
});

// Go to the last page when a new item is added
const updatePaginationAfterAdd = () => {
  currentPage.value = totalPages.value;
};

definePageMeta({
  layout: "admin",
});
</script>
