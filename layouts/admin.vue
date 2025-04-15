<template>
  <div class="min-h-screen flex flex-col">
    <Navbar />
    <div class="flex flex-1">
      <AdminSidebar />
      <main class="flex-1 bg-gray-50 overflow-y-auto p-6">
        <slot />
      </main>
    </div>
  </div>
</template>

<script setup>
import Navbar from "~/components/Navbar.vue";
import AdminSidebar from "../components/AdminSidebar.vue";
</script>

<style scoped>
main::-webkit-scrollbar {
  width: 6px;
}
main::-webkit-scrollbar-thumb {
  background-color: #d1d5db;
  border-radius: 6px;
}
main::-webkit-scrollbar-thumb:hover {
  background-color: #9ca3af;
}
</style>
