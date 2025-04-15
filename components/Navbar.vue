<template>
  <nav
    class="bg-white p-4 flex items-center justify-between w-full sticky top-0 z-10"
  >
    <div class="flex items-center">
      <h3 class="text-lg font-bold text-gray-800 uppercase">Hello Admin,</h3>
    </div>
    <button
      class="flex items-center gap-2 px-4 py-2 rounded-lg text-orange-600 hover:bg-orange-50 transition-colors duration-200"
      @click="handleLogout"
    >
      <LogOut class="w-5 h-5" />
      <span class="text-sm font-medium uppercase">Logout</span>
    </button>
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
