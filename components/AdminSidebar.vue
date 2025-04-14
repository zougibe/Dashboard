<template>
  <aside class="w-60 min-h-screen bg-white border-r">
    <div class="p-6 flex items-center gap-2">
      <img
        src="~/assets/logo/image.png"
        alt="Home Chefs Logo"
        class="w-8 h-8"
      />
      <h1 class="text-lg font-bold text-gray-800 uppercase">Home Chefs</h1>
    </div>
    <nav class="px-4 space-y-2 mt-4">
      <NuxtLink
        v-for="item in navItems"
        :key="item.label"
        :to="item.to"
        class="flex items-center gap-3 px-4 py-2 rounded-lg transition-colors duration-200 hover:bg-orange-50"
        :class="{
          'bg-orange-100 text-orange-600': route.path === item.to,
        }"
        active-class="bg-orange-100 text-orange-600"
      >
        <component :is="item.icon" class="w-6 h-6" />
        <span class="text-sm font-medium uppercase tracking-wide">{{
          item.label
        }}</span>
      </NuxtLink>
    </nav>
  </aside>
</template>

<script setup>
import {
  Home,
  User,
  Pizza,
  ShoppingCart,
  Utensils,
  Users,
} from "lucide-vue-next";

const navItems = [
  { label: "Home", to: "/admin", icon: Home },
  { label: "Chefs", to: "/admin/chefs", icon: User },
  { label: "Recipes", to: "/admin/recipes", icon: Pizza },
  { label: "Orders", to: "/admin/orders", icon: ShoppingCart },
  { label: "Categories", to: "/admin/categories", icon: Utensils },
  { label: "Customers", to: "/admin/customers", icon: Users },
];

const route = useRoute();
</script>

<style scoped>
aside {
  border-right: 1px solid #e5e7eb;
}

nav a {
  color: #6b7280;
}

nav a:hover {
  color: #ea580c;
}

nav a:hover svg {
  stroke: #ea580c;
}

.active-class {
  background-color: #fff7ed;
  color: #ea580c;
}
</style>
