<template>
  <aside class="w-60 min-h-screen bg-white border-r">
    <div class="p-6 flex items-center gap-2">
      <img
        src="../assets/images/logo2.svg"
        alt="Home Chefs Logo"
        class="w-20 h-20"
      />
    </div>
    <nav class="px-4 space-y-2 mt-4">
      <div>
        <h3 class="px-4 font-medium text-orange-600 py-[8px]">
          {{ role }} Roles
        </h3>
        <NuxtLink
          v-for="item in filteredNavItems"
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
      </div>
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

// Reactive role state (default to 'Admin')
const role = ref("Admin");

// All possible navigation items
const allNavItems = [
  { label: "Home", to: "/admin/", icon: Home, roles: ["Admin", "Chef"] },
  { label: "Chefs", to: "/admin/chefs", icon: User, roles: ["Admin"] },
  {
    label: "Categories",
    to: "/admin/categories",
    icon: Utensils,
    roles: ["Admin"],
  },
  {
    label: "Recipes",
    to: "/admin/recipes",
    icon: Pizza,
    roles: ["Admin", "Chef"],
  },
  { label: "Customers", to: "/admin/customers", icon: Users, roles: ["Admin"] },
  {
    label: "Orders",
    to: "/admin/orders",
    icon: ShoppingCart,
    roles: ["Admin", "Chef"],
  },
];

// Computed property to filter nav items based on current role
const filteredNavItems = computed(() => {
  return allNavItems.filter((item) => item.roles.includes(role.value));
});

// Function to toggle between roles (you can call this from parent or based on auth)
const toggleRole = () => {
  role.value = role.value === "Admin" ? "Chef" : "Admin";
};

const route = useRoute();

// Expose the toggle function to parent component if needed
defineExpose({
  toggleRole,
  role,
});
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
