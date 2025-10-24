<template>
  <div class="fixed inset-0 bg-black bg-opacity-40 flex items-center justify-center">
    <div class="bg-white rounded-lg shadow p-6 w-96">
      <h2 class="text-xl font-semibold mb-4">Add New Task</h2>
      <form @submit.prevent="saveTask">
        <input
          v-model="task.title"
          type="text"
          placeholder="Enter task title"
          class="border w-full p-2 rounded mb-4"
          required
        />

        <div class="flex justify-end space-x-2">
          <button
            type="button"
            @click="$emit('close')"
            class="bg-gray-300 px-4 py-2 rounded"
          >
            Cancel
          </button>
          <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded">
            Save
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const emit = defineEmits(["save", "close"]);

const task = ref({ title: "" });

const saveTask = () => {
  emit("save", task.value);
  task.value.title = "";
};
</script>
