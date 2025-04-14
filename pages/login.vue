<template>
  <div
    class="min-h-screen flex items-center justify-center bg-cover bg-no-repeat bg-center"
    style="
      background-image: url('https://images.unsplash.com/photo-1555939594-58d7cb561ad1?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D');
    "
  >
    <div class="max-w-md w-full bg-white p-8 rounded-lg shadow-lg">
      <NuxtLink to="/">
        <!-- <img src="/images/logo2.svg" alt="Logo" class="w-32 mb-8 mx-auto" /> -->
      </NuxtLink>
      <h2 class="text-3xl font-bold mb-8 text-gray-800 text-center">
        Welcome to Chefs Admin Dashboard
      </h2>
      <form @submit.prevent="handleLogin" class="space-y-6">
        <div class="space-y-2">
          <label class="block text-gray-700 font-medium">Email Address</label>
          <input
            v-model="form.email"
            type="email"
            placeholder="Enter your email..."
            required
            class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500"
          />
        </div>
        <div class="space-y-2 relative">
          <label class="block text-gray-700 font-medium">Password</label>
          <div class="relative">
            <input
              v-model="form.password"
              :type="showPassword ? 'text' : 'password'"
              placeholder="Enter your password..."
              required
              class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 pr-10"
            />
            <button
              type="button"
              @click="togglePasswordVisibility"
              class="absolute right-3 top-3 text-gray-500 hover:text-gray-700"
            >
              <i :class="showPassword ? 'fas fa-eye-slash' : 'fas fa-eye'"></i>
            </button>
          </div>
        </div>
        <div class="text-right">
          <NuxtLink
            to="/auth/forgetPassword"
            class="text-orange-500 text-sm hover:underline"
          >
            Forgot Password?
          </NuxtLink>
        </div>
        <button
          type="submit"
          class="w-full bg-orange-500 text-white py-3 rounded-lg hover:bg-orange-600 transition-colors font-medium"
        >
          Login
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const form = ref({
  email: "",
  password: "",
});

// Password visibility state
const showPassword = ref(false);

const togglePasswordVisibility = () => {
  showPassword.value = !showPassword.value;
};

const handleLogin = () => {
  console.log("Form data:", form.value);
  // Add your login logic here
};

definePageMeta({
  layout: "auth",
});
</script>
