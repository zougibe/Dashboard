<template>
  <div class="p-4">
    <!-- Header -->
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold">Categories</h2>
      <button
        @click="openModal()"
        class="px-4 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
      >
        Add Category
      </button>
    </div>

    <!-- Table -->
    <div class="bg-white rounded-lg shadow overflow-hidden">
      <CategoriesTable
        :titles="titles"
        :categories="paginatedCategories"
        @delete-category="deleteCategory"
        @edit-category="editCategory"
      />
    </div>

    <!-- Pagination -->
    <div class="flex justify-center items-center gap-2 p-4 border-t border-gray-200">
      <button @click="goToPage(currentPage - 1)" :disabled="currentPage === 1"
        class="p-2 rounded-full hover:bg-gray-200 disabled:opacity-50">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
        </svg>
      </button>

      <template v-for="page in visiblePages" :key="page">
        <button
          v-if="page !== '...'" @click="goToPage(page)"
          :class="[
            'px-3 py-1 rounded-full text-sm font-medium',
            currentPage === page
              ? 'bg-orange-500 text-white'
              : 'bg-gray-100 text-gray-800 hover:bg-orange-100'
          ]"
        >{{ page }}</button>
        <span v-else class="px-2 text-gray-500">...</span>
      </template>

      <button @click="goToPage(currentPage + 1)" :disabled="currentPage === totalPages"
        class="p-2 rounded-full hover:bg-gray-200 disabled:opacity-50">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </button>
    </div>

    <!-- Modal -->
    <div v-if="showModal" class="fixed inset-0  bg-opacity-50 flex items-center justify-center z-50">
      <div class="bg-white rounded-xl shadow-xl p-6 w-[90%] max-w-lg relative">
        <button @click="closeModal" class="absolute top-3 right-3 text-gray-400 hover:text-gray-600 text-xl font-bold">
          &times;
        </button>
        <h2 class="text-2xl font-bold mb-6">{{ isEditing ? 'Edit' : 'Add New' }} Category</h2>

        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium mb-1">Category Name</label>
            <input v-model="newCategory.categoryName" type="text"
              class=" text-gray-500 w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400 " />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Image URL</label>
            <input v-model="newCategory.image" type="text"
              class=" text-gray-500 w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400" />
          </div>
        </div>

        <div class="mt-6">
          <button @click="saveCategory"
            class="w-full bg-orange-500 hover:bg-orange-600 text-white font-medium px-4 py-2 rounded-lg transition">
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import CategoriesTable from "../../components/CategoriesTable";

const titles = [
  { val1: "Category Name", val2: "Image", val3: "Action" }
];

const categories = ref([
  { categoryName: "FastFood", image: "link" },
  { categoryName: "Asian", image: "link" },
  { categoryName: "Healthy", image: "link" },
  { categoryName: "Dessert", image: "link" },
  { categoryName: "BBQ", image: "link" },
  { categoryName: "Vegan", image: "link" }
]);

const showModal = ref(false);
const newCategory = ref({ categoryName: "", image: "" });
const editingIndex = ref(null);
const isEditing = computed(() => editingIndex.value !== null);

const currentPage = ref(1);
const itemsPerPage = 4;

const totalPages = computed(() => Math.ceil(categories.value.length / itemsPerPage));

const paginatedCategories = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return categories.value.slice(start, start + itemsPerPage);
});

const visiblePages = computed(() => {
  const pages = [];
  const max = totalPages.value;
  const current = currentPage.value;

  if (max <= 7) {
    for (let i = 1; i <= max; i++) pages.push(i);
  } else {
    pages.push(1);
    if (current > 4) pages.push('...');
    for (let i = Math.max(2, current - 2); i <= Math.min(max - 1, current + 2); i++) {
      pages.push(i);
    }
    if (current < max - 3) pages.push('...');
    pages.push(max);
  }

  return pages;
});

const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

const openModal = () => {
  newCategory.value = { categoryName: "", image: "" };
  editingIndex.value = null;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
  newCategory.value = { categoryName: "", image: "" };
  editingIndex.value = null;
};

const saveCategory = () => {
  if (!newCategory.value.categoryName || !newCategory.value.image) return;

  if (isEditing.value) {
    categories.value[editingIndex.value] = { ...newCategory.value };
  } else {
    categories.value.push({ ...newCategory.value });
  }

  closeModal();
};

const deleteCategory = (paginatedIndex) => {
  const actualIndex = (currentPage.value - 1) * itemsPerPage + paginatedIndex;
  categories.value.splice(actualIndex, 1);

  // If current page became empty, go to previous page
  if (paginatedCategories.value.length === 0 && currentPage.value > 1) {
    currentPage.value--;
  }
};

const editCategory = (paginatedIndex) => {
  const actualIndex = (currentPage.value - 1) * itemsPerPage + paginatedIndex;
  const item = categories.value[actualIndex];
  newCategory.value = { ...item };
  editingIndex.value = actualIndex;
  showModal.value = true;
};

definePageMeta({
  layout: "admin",
});
</script>
