<template>
  <div>
    <button
      @click="openModal"
      class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700"
    >
      + Add Task
    </button>

    <TaskModal v-if="showModal" @close="closeModal" @save="addTask" />

    <ul class="mt-6 space-y-3">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @delete="deleteTask(task.id)"
        @toggle="toggleComplete(task.id, task.completed)"
      />
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { db } from "../lib/firebase";
import {
  collection,
  addDoc,
  getDocs,
  updateDoc,
  doc,
  deleteDoc,
} from "firebase/firestore";
import TaskModal from "./TaskModal.vue";
import TaskItem from "./TaskItem.vue";

const tasks = ref([]);
const showModal = ref(false);
const tasksRef = collection(db, "tasks");

const fetchTasks = async () => {
  const querySnapshot = await getDocs(tasksRef);
  tasks.value = querySnapshot.docs.map((doc) => ({
    id: doc.id,
    ...doc.data(),
  }));
};

const addTask = async (task) => {
  await addDoc(tasksRef, { ...task, completed: false });
  await fetchTasks();
  closeModal();
};

const toggleComplete = async (id, completed) => {
  const docRef = doc(db, "tasks", id);
  await updateDoc(docRef, { completed: !completed });
  fetchTasks();
};

const deleteTask = async (id) => {
  await deleteDoc(doc(db, "tasks", id));
  fetchTasks();
};

const openModal = () => (showModal.value = true);
const closeModal = () => (showModal.value = false);

onMounted(fetchTasks);
</script>
