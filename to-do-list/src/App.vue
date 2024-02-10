<script setup>
import { reactive, onMounted } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import TaskList from "./components/TaskList.vue";

import "./app.css";

const state = reactive({
  filter: "all",
  tempTask: "",
  tasks: [],
});

const getPendingTasks = () => {
  return state.tasks.filter((task) => !task.completed);
};

const getCompletedTasks = () => {
  return state.tasks.filter((task) => task.completed);
};

const getFilteredTasks = () => {
  const { filter } = state;
  switch (filter) {
    case "pending":
      return getPendingTasks();
    case "completed":
      return getCompletedTasks();
    default:
      return state.tasks;
  }
};

const addTask = () => {
  const options = { month: "short", day: "numeric", year: "numeric" };
  const newTask = {
    title: state.tempTask,
    completed: false,
    date: new Date().toLocaleDateString("en-US", options),
  };
  state.tasks.push(newTask);
  state.tempTask = "";
  updateLocalStorage();
};

const updateLocalStorage = () => {
  localStorage.setItem("tasks", JSON.stringify(state.tasks));
};

const handleUpdateTaskStatus = ({ task, completed }) => {
  task.completed = completed;
  updateLocalStorage();
};

const deleteTask = (taskToDelete) => {
  state.tasks = state.tasks.filter((task) => task !== taskToDelete);
  updateLocalStorage();
};

onMounted(() => {
  const storedTasks = localStorage.getItem("tasks");
  if (storedTasks) {
    state.tasks = JSON.parse(storedTasks);
  }
});
</script>

<template>
  <div class="container">
    <Header :pending-tasks="getPendingTasks().length" />
    <Form
      :change-filter="(event) => (state.filter = event.target.value)"
      :temp-task="state.tempTask"
      :edit-temp-task="(event) => (state.tempTask = event.target.value)"
      :add-task="addTask"
    />
    <TaskList
      :tasks="getFilteredTasks()"
      @update-task-status="handleUpdateTaskStatus"
      @delete-task="deleteTask"
    />
  </div>
</template>