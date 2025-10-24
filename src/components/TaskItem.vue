<template>
  <li
    class="flex justify-between items-center bg-gray-50 border p-3 rounded-lg"
  >
    <div>
      <input
        type="checkbox"
        class="mr-3"
        :checked="task.completed"
        @change="$emit('toggle')"
      />
      <span :class="{ 'line-through text-gray-500': task.completed }">
        {{ task.title }}
      </span>
    </div>

    <button
      @click="$emit('delete')"
      class="text-red-600 hover:underline text-sm"
    >
      Delete
    </button>
  </li>
</template>

<script setup>
defineProps({ task: Object });
defineEmits(["toggle", "delete"]);
</script>
