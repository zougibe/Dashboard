<template>
  <div class="overflow-x-auto">
    <table class="min-w-full text-sm text-left text-gray-700">
      <thead class="bg-gray-100 text-xs uppercase">
        <tr v-for="(title, index) in titles" :key="index">
          <th scope="col" class="px-6 py-3">{{ title.val1 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val2 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val3 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val4 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val5 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val6 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val7 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val8 }}</th>
          <th scope="col" class="px-6 py-3">{{ title.val9 }}</th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(recipe, index) in recipes"
          :key="index"
          class="border-b border-gray-300 hover:bg-gray-50"
        >
          <td class="px-6 py-4">{{ recipe.recipeName }}</td>
          <td class="px-6 py-4">{{ recipe.duration }}</td>
          <td class="px-6 py-4">{{ recipe.ingredient }}</td>
          <td class="px-6 py-4">{{ recipe.category }}</td>
          <td class="px-6 py-4">{{ recipe.video }}</td>
          <td class="px-6 py-4">{{ recipe.image }}</td>
          <td class="px-6 py-4">{{ recipe.rate }}</td>
          <td class="px-6 py-4">{{ recipe.description }}</td>
          <td class="px-6 py-4">
            <div class="flex gap-2">
              <button
                @click="openEditModal(recipe, index)"
                class="bg-green-500 text-white px-4 py-2 rounded-md hover:bg-green-600"
              >
                Edit
              </button>
              <button
                @click="deleteRecipe(index)"
                class="bg-red-500 text-white px-4 py-2 rounded-md hover:bg-red-600"
              >
                Delete
              </button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- Edit Modal -->
  <div
    v-if="isEditModalOpen"
    class="fixed inset-0 bg-opacity-50 flex items-center justify-center z-50"
  >
    <div class="bg-white p-6 rounded-lg w-full sm:max-w-lg relative">
      <button
        @click="closeEditModal"
        class="absolute top-2 right-2 text-gray-500 hover:text-gray-700 text-xl font-bold"
      >
        &times;
      </button>
      <h2 class="text-2xl font-bold mb-6 text-start text-gray-700">
        Edit Recipe
      </h2>

      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Recipe Name</label
          >
          <input
            v-model="editedRecipe.recipeName"
            type="text"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Duration</label
          >
          <input
            v-model="editedRecipe.duration"
            type="text"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Ingredients</label
          >
          <input
            v-model="editedRecipe.ingredient"
            type="text"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Category</label
          >
          <input
            v-model="editedRecipe.category"
            type="text"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Video URL</label
          >
          <input
            v-model="editedRecipe.video"
            type="text"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Image URL</label
          >
          <input
            v-model="editedRecipe.image"
            type="text"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700">Rate</label>
          <input
            v-model="editedRecipe.rate"
            type="number"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700"
            >Description</label
          >
          <textarea
            v-model="editedRecipe.description"
            rows="3"
            class="w-full p-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-orange-400 text-gray-600"
          ></textarea>
        </div>
      </div>

      <div class="mt-6 flex justify-end">
        <button
          @click="saveEditedRecipe"
          class="w-full bg-orange-500 hover:bg-orange-600 text-white font-medium px-6 py-2 rounded-lg transition"
        >
          Save
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  recipes: {
    type: Array,
    required: true,
    default: () => [],
  },
  titles: {
    type: Array,
    required: true,
    default: () => [],
  },
});

const emit = defineEmits(["delete-recipe"]);

const isEditModalOpen = ref(false);
const editedRecipe = ref({});

const openEditModal = (recipe, index) => {
  editedRecipe.value = { ...recipe, index };
  isEditModalOpen.value = true;
};

const closeEditModal = () => {
  isEditModalOpen.value = false;
  editedRecipe.value = {};
};

const saveEditedRecipe = () => {
  const index = editedRecipe.value.index;
  props.recipes[index] = { ...editedRecipe.value };
  closeEditModal();
};

const deleteRecipe = (index) => {
  emit("delete-recipe", index);
};
</script>
