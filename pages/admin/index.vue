<template>
  <div class="space-y-6 p-4">
    <!-- Dashboard Cards -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
      <DashboardCard title="Orders" value="68" unit="Order(s)" />
      <DashboardCard title="Recipes" value="5" unit="Recipe(s)" />
      <DashboardCard title="Chefs" value="14" unit="Chef(s)" />
      <DashboardCard title="Customers" value="150" unit="User(s)" />
    </div>

    <!-- Recent Orders Table -->
    <div class="bg-white rounded-lg shadow overflow-hidden">
      <div class="p-4 border-b border-gray-200">
        <h2 class="text-lg font-semibold">Recent Orders</h2>
      </div>

      <!-- Table -->
      <RecentOrdersTable :titles="titles" :orders="paginatedOrders" />

      <!-- Pagination -->
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
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import DashboardCard from '../../components/DashboardCard.vue';
import RecentOrdersTable from '../../components/RecentOrdersTable.vue';

definePageMeta({
  layout: 'admin',
});

const titles = [
  {
    val1: "Customer Name",
    val2: "Recipes Name",
    val3: "Payment Method",
    val4: "Total Cost",
    val5: "Address",
    val6: "Phone Number",
    val7: "Notes",
    val8: "Order Status",
    val9: "Actions",
  },
];

const orders = ref([
  {
    customerName: "Muhammad Salah",
    recipeName: "Pizza",
    paymentMethod: "Online Payment",
    total: "250.00 LE",
    address: "Ismailia",
    phone: "01068687747",
    notes: "Not Spicy",
    status: "in progress",
  },
  {
    customerName: "Fatma Hamed",
    recipeName: "Salad Bowl",
    paymentMethod: "Cash on Delivery",
    total: "85.00 LE",
    address: "Cairo",
    phone: "01122334455",
    notes: "-",
    status: "in progress",
  },
  {
    customerName: "Ahmed Samir",
    recipeName: "Burger",
    paymentMethod: "Cash on Delivery",
    total: "120.00 LE",
    address: "Giza",
    phone: "01234567890",
    notes: "Extra cheese",
    status: "pending",
  },
  {
    customerName: "Nour Ali",
    recipeName: "Pasta",
    paymentMethod: "Online Payment",
    total: "150.00 LE",
    address: "Alexandria",
    phone: "01012345678",
    notes: "No garlic",
    status: "in progress",
  },
  {
    customerName: "Omar Khaled",
    recipeName: "Fried Chicken",
    paymentMethod: "Cash on Delivery",
    total: "200.00 LE",
    address: "Tanta",
    phone: "01198765432",
    notes: "-",
    status: "in progress",
  },
  {
    customerName: "Sara Youssef",
    recipeName: "Soup",
    paymentMethod: "Online Payment",
    total: "60.00 LE",
    address: "Mansoura",
    phone: "01511223344",
    notes: "-",
    status: "pending",
  },
]);

// Pagination logic
const currentPage = ref(1);
const itemsPerPage = 3;

const totalPages = computed(() => Math.ceil(orders.value.length / itemsPerPage));

const paginatedOrders = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return orders.value.slice(start, start + itemsPerPage);
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
    for (let i = Math.max(2, current - 1); i <= Math.min(max - 1, current + 1); i++) {
      pages.push(i);
    }
    if (current < max - 3) pages.push('...');
    pages.push(max);
  }

  return pages;
});
</script>
