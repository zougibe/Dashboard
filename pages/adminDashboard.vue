<template>
  <div class="flex h-screen bg-gray-100">
    <!-- Sidebar -->
    <aside class="w-64 bg-white border-r">
      <div class="flex items-center justify-center h-16 border-b p-4">
        <span class="text-xl font-semibold ml-2">Admin Dashboard</span>
      </div>
      <nav class="mt-4">
        <ul>
          <li v-for="item in navItems" :key="item.label">
            <NuxtLink
              :to="item.to"
              class="flex items-center px-4 py-3 text-gray-700 hover:bg-orange-100 hover:text-orange-600"
              :class="{
                'bg-orange-100 text-orange-600': item.label === 'Home',
              }"
            >
              <component :is="item.icon" class="w-5 h-5 mr-3" />
              {{ item.label }}
            </NuxtLink>
          </li>
        </ul>
      </nav>
    </aside>

    <!-- Main Content -->
    <main class="flex-1 overflow-y-auto p-6">
      <div class="flex justify-between items-center mb-6">
        <h1 class="text-2xl font-bold">Admin Dashboard</h1>
        <button class="text-red-600 flex items-center space-x-1">
          <IconLogout class="w-5 h-5" />
          <span>Logout</span>
        </button>
      </div>

      <!-- Statistics Cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-10">
        <DashboardCard title="Orders" value="2,000" unit="Orders" />
        <DashboardCard title="Recipes" value="850" unit="Recipes" />
        <DashboardCard title="Chefs" value="50" unit="Chefs" />
        <DashboardCard title="Customers" value="1,000" unit="User" />
      </div>

      <!-- Recent Orders -->
      <section>
        <h2 class="text-xl font-semibold mb-4">Recent Orders</h2>
        <div class="overflow-x-auto">
          <table class="min-w-full bg-white border">
            <thead class="bg-gray-100">
              <tr>
                <th class="px-4 py-2 text-left text-sm font-semibold">
                  Customer name
                </th>
                <th class="px-4 py-2 text-left text-sm font-semibold">
                  Recipe name
                </th>
                <th class="px-4 py-2 text-left text-sm font-semibold">
                  Payment method
                </th>
                <th class="px-4 py-2 text-left text-sm font-semibold">Total</th>
                <th class="px-4 py-2 text-left text-sm font-semibold">
                  Address
                </th>
                <th class="px-4 py-2 text-left text-sm font-semibold">
                  Phone number
                </th>
                <th class="px-4 py-2 text-left text-sm font-semibold">Notes</th>
                <th class="px-4 py-2 text-left text-sm font-semibold">
                  Order status
                </th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="order in recentOrders"
                :key="order.id"
                class="border-t hover:bg-gray-50"
              >
                <td class="px-4 py-2">{{ order.customer }}</td>
                <td class="px-4 py-2">{{ order.recipe }}</td>
                <td class="px-4 py-2">{{ order.payment }}</td>
                <td class="px-4 py-2">{{ order.total }}</td>
                <td class="px-4 py-2">{{ order.address }}</td>
                <td class="px-4 py-2">{{ order.phone }}</td>
                <td class="px-4 py-2">{{ order.notes }}</td>
                <td class="px-4 py-2">{{ order.status }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { IconLogout } from "lucide-vue-next";
import { Home, User, ChefHat, List, ShoppingCart } from "lucide-vue-next";
import DashboardCard from "@/components/DashboardCard.vue";

const navItems = [
  { label: "Home", icon: Home, to: "/" },
  { label: "Chefs", icon: ChefHat, to: "/chefs" },
  { label: "Recipes", icon: List, to: "/recipes" },
  { label: "Orders", icon: ShoppingCart, to: "/orders" },
  { label: "Categories", icon: List, to: "/categories" },
  { label: "Customers", icon: User, to: "/customers" },
];

const recentOrders = Array(8).fill({
  id: Math.random(),
  customer: "Muhammad Salah",
  recipe: "Pizza",
  payment: "Online Payment",
  total: "250.00 LE",
  address: "Ismailia",
  phone: "01068687747",
  notes: "Not Spicy",
  status: "in progress",
});
</script>

<style scoped>
th,
td {
  white-space: nowrap;
}
</style>
