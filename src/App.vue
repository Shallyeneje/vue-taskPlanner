<template>
  <div class="min-h-screen bg-gray-100 p-6">
    <div class="max-w-3xl mx-auto bg-white rounded-xl shadow p-6">
      <h1 class="text-2xl font-bold mb-4 text-center">Task Planner</h1>

      <TaskList />
    </div>
  </div>
</template>

<script setup>
import TaskList from "./components/TaskList.vue";
</script>
