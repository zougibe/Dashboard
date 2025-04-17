<template>
  <div class="p-4 relative">
    <!-- Header and Add Button -->
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold text-gray-800">Chefs</h2>
      <button
        @click="openModal()"
        class="px-4 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
      >
        Add Chef
      </button>
    </div>

    <!-- Table Section -->
    <div class="bg-white rounded-lg shadow overflow-hidden">
      <ChefsTable
        :titles="titles"
        :chefs="paginatedChefs"
        @edit-chef="editChef"
        @delete-chef="deleteChef"
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

    <!-- Chef Modal (Add/Edit) -->
    <div
      v-if="showModal"
      class="fixed inset-0 bg-opacity-50 flex items-center justify-center z-50"
    >
      <div
        class="bg-white rounded-xl shadow-xl p-6 w-[90%] max-w-lg relative z-50"
      >
        <!-- Close Button (X) -->
        <button
          @click="closeModal"
          class="absolute top-3 right-3 text-gray-400 hover:text-gray-600 text-xl font-bold"
        >
          ×
        </button>

        <h2 class="text-2xl font-bold text-gray-800 mb-6">
          {{ isEditing ? "Edit Chef" : "Add New Chef" }}
        </h2>

        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
              >Chef Name</label
            >
            <input
              v-model="newChef.name"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-500"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
              >Title</label
            >
            <input
              v-model="newChef.title"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-500"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
              >Image Link</label
            >
            <input
              v-model="newChef.image"
              type="text"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-500"
            />
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
              >Short Bio</label
            >
            <textarea
              v-model="newChef.bio"
              rows="3"
              class="w-full border border-gray-300 rounded-lg p-2 focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-500"
            ></textarea>
          </div>
        </div>

        <!-- Save Button (Full Width) -->
        <div class="mt-6">
          <button
            @click="saveChef"
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

const chefs = ref([
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
    ChefName: "Mohamed",
    recipeName: "Healthy",
    bio: "28 year old",
    totalR: "22",
    totalO: "214",
    rate: "4.1",
    image: "link",
  },
  {
    ChefName: "Huessien",
    recipeName: "Seafood",
    bio: "43 year old",
    totalR: "32",
    totalO: "157",
    rate: "4.5",
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
    ChefName: "Mohamed",
    recipeName: "Healthy",
    bio: "28 year old",
    totalR: "22",
    totalO: "214",
    rate: "4.1",
    image: "link",
  },
  {
    ChefName: "Huessien",
    recipeName: "Seafood",
    bio: "43 year old",
    totalR: "32",
    totalO: "157",
    rate: "4.5",
    image: "link",
  },
]);

const showModal = ref(false);
const currentPage = ref(1);
const itemsPerPage = 4;
const newChef = ref({
  name: "",
  title: "",
  image: "",
  bio: "",
});
const editingIndex = ref(null);
const isEditing = computed(() => editingIndex.value !== null);

const totalPages = computed(() => Math.ceil(chefs.value.length / itemsPerPage));

const paginatedChefs = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return chefs.value.slice(start, start + itemsPerPage);
});

const goToPage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

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

const openModal = () => {
  newChef.value = { name: "", title: "", image: "", bio: "" };
  editingIndex.value = null;
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
  newChef.value = { name: "", title: "", image: "", bio: "" };
  editingIndex.value = null;
};

const saveChef = () => {
  if (
    !newChef.value.name ||
    !newChef.value.title ||
    !newChef.value.image ||
    !newChef.value.bio
  )
    return;

  if (isEditing.value) {
    const actualIndex = editingIndex.value;
    chefs.value[actualIndex] = {
      ChefName: newChef.value.name,
      recipeName: newChef.value.title,
      bio: newChef.value.bio,
      totalR: chefs.value[actualIndex].totalR,
      totalO: chefs.value[actualIndex].totalO,
      rate: chefs.value[actualIndex].rate,
      image: newChef.value.image,
    };
  } else {
    chefs.value.push({
      ChefName: newChef.value.name,
      recipeName: newChef.value.title,
      bio: newChef.value.bio,
      totalR: "0",
      totalO: "0",
      rate: "0",
      image: newChef.value.image,
    });
  }

  closeModal();
};

const deleteChef = (paginatedIndex) => {
  const actualIndex = (currentPage.value - 1) * itemsPerPage + paginatedIndex;
  chefs.value.splice(actualIndex, 1);
  // Adjust currentPage if the current page is empty
  if (paginatedChefs.value.length === 0 && currentPage.value > 1) {
    currentPage.value--;
  }
};

const editChef = (paginatedIndex) => {
  const actualIndex = (currentPage.value - 1) * itemsPerPage + paginatedIndex;
  const chef = chefs.value[actualIndex];
  newChef.value = {
    name: chef.ChefName,
    title: chef.recipeName,
    image: chef.image,
    bio: chef.bio,
  };
  editingIndex.value = actualIndex;
  showModal.value = true;
};

definePageMeta({
  layout: "admin",
});
</script>
