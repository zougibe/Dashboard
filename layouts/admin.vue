<template>
  <div class="flex min-h-screen">
    <AdminSidebar />
    <main class="flex-1 bg-gray-50 p-6 overflow-y-auto">
      <slot />
    </main>
  </div>
</template>

<script setup>
import AdminSidebar from "../components/AdminSidebar.vue";
</script>

<style scoped>
main::-webkit-scrollbar {
  width: 6px;
}
main::-webkit-scrollbar-thumb {
  background-color: #e2e8f0;
  border-radius: 6px;
}
</style>
