<template>
  <nav
    class="bg-white flex items-between justify-between w-full sticky top-0 z-10"
  >
    <div class="flex items-center gap-2 pl-2">
      <img
        src="../assets/images/logo2.svg"
        class="w-[80px] h-[73px] mr-1 text-center"
        alt="Home Chefs Logo"
      />
      <h2 class="text-lg font-bold text-gray-800 uppercase">
        <span class="text-orange-500">Admin</span> Dashboard
      </h2>
    </div>
    <div class="flex items-center">
      <h3 class="">Hello Admin,</h3>
      <button
        class="flex items-center gap-2 px-4 py-2 rounded-lg text-orange-600 hover:bg-orange-50 transition-colors duration-200"
        @click="handleLogout"
      >
        <LogOut class="w-5 h-5" />
        <span class="text-sm font-medium uppercase">Logout</span>
      </button>
    </div>
  </nav>
</template>

<script setup>
import { LogOut } from "lucide-vue-next";

const handleLogout = () => {
  console.log("Logout clicked");
  navigateTo("/login");
};
</script>

<style scoped>
nav {
  border-bottom: 1px solid #e5e7eb;
}
</style>
