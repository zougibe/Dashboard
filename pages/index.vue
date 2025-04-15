<template>
  <div class="space-y-8 p-3">
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
      <DashboardCard title="Orders" value="68" unit="Order(s)" />
      <DashboardCard title="Recipes" value="5" unit="Recipe(s)" />
      <DashboardCard title="Chefs" value="14" unit="Chef(s)" />
      <DashboardCard title="Customers" value="150" unit="User(s)" />
    </div>

    <div>
      <h2 class="text-lg font-semibold mb-4">Recent Orders</h2>
      <RecentOrdersTable :orders="orders" />
    </div>
  </div>
</template>

<script setup>
import DashboardCard from "../../components/DashboardCard.vue";
import RecentOrdersTable from "../../components/RecentOrdersTable.vue";

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
