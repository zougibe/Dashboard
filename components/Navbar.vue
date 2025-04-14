<template>
  <nav class="bg-white p-3 flex items-center justify-between">
    <div class="flex items-center">
      <h3 class="text-lg font-bold text-gray-800 uppercase">Hello Admin,</h3>
    </div>
    <button
      class="flex items-center gap-1 text-orange-600 hover:text-orange-700 transition-colors duration-200"
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
  // Add your logout logic here
  console.log("Logout clicked");
};
</script>
