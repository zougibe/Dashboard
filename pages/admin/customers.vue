<template>
  <div class="p-4">
    <!-- Header and Add Button -->
    <div class="flex justify-between items-center mb-6">
      <h2 class="text-lg font-semibold">Users</h2>
    </div>

    <!-- Table Section -->
    <div class="bg-white rounded-lg shadow overflow-hidden">
      <UsersTable :titles="titles" :users="paginatedUsers" @deleteUser="deleteUser" />
    </div>

    <!-- Pagination Section -->
    <div class="flex justify-center items-center gap-2 p-4 border-t border-gray-200">
      <!-- Prev Button -->
      <button
        @click="goToPage(currentPage - 1)"
        :disabled="currentPage === 1"
        class="p-2 rounded-full hover:bg-gray-200 disabled:opacity-50"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
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
              : 'bg-gray-100 text-gray-800 hover:bg-orange-100'
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
        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import UsersTable from "../../components/UsersTable";

const titles = [
  {
    val1: "Customer Name",
    val2: "Email",
    val3: "Phone Number",
    val4: "Action",
  },
];

const users = ref([
  {
    userName: "Ahmed Zougibe",
    email: "ahmed.zougibe@gmail.com",
    phoneNumber: "01030003913",
  },
  {
    userName: "Mona Ali",
    email: "mona.ali@gmail.com",
    phoneNumber: "01021478563",
  },
  {
    userName: "Sammy Mohamed",
    email: "sammy.mohamed@gmail.com",
    phoneNumber: "01124567892",
  },
  {
    userName: "Sara Ahmed",
    email: "sara.ahmed@yahoo.com",
    phoneNumber: "01235678945",
  },
  {
    userName: "Mohamed Gamal",
    email: "mohamed.gamal@hotmail.com",
    phoneNumber: "01023874659",
  },
  {
    userName: "Laila Hossam",
    email: "laila.hossam@outlook.com",
    phoneNumber: "01198765432",
  },
]);

const showModal = ref(false);
const currentPage = ref(1);
const itemsPerPage = 4;

const totalPages = computed(() => Math.ceil(users.value.length / itemsPerPage));

const paginatedUsers = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return users.value.slice(start, start + itemsPerPage);
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
    if (current > 4) pages.push('...');
    for (let i = Math.max(2, current - 2); i <= Math.min(max - 1, current + 2); i++) {
      pages.push(i);
    }
    if (current < max - 3) pages.push('...');
    pages.push(max);
  }

  return pages;
});

// Handle delete
const deleteUser = (index) => {
  users.value.splice(index, 1);
};

definePageMeta({
  layout: "admin",
});
</script>
