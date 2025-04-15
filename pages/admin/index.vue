<template>
  <div class="space-y-6 p-4">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
      <DashboardCard title="Orders" value="68" unit="Order(s)" />
      <DashboardCard title="Recipes" value="5" unit="Recipe(s)" />
      <DashboardCard title="Chefs" value="14" unit="Chef(s)" />
      <DashboardCard title="Customers" value="150" unit="User(s)" />
    </div>

    <div class="bg-white rounded-lg shadow overflow-hidden">
      <div class="p-4 border-b border-gray-200">
        <h2 class="text-lg font-semibold">Recent Orders</h2>
      </div>
      <RecentOrdersTable :titles="titles" :orders="orders" />
    </div>
  </div>
</template>

<script setup>
import DashboardCard from "../../components/DashboardCard.vue";
import RecentOrdersTable from "../../components/RecentOrdersTable";

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

const orders = [
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
    status: "completed",
  },
];

definePageMeta({
  layout: "admin",
});
</script>
