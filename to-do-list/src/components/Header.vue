<script setup>
import Logo from "../assests/logo.jpg";
const props = defineProps(["pendingTasks"]);
</script>

<template>
  <header
    class="p-3 mb-4 mt-4 bg-light rounded-3 shadow-sm"
    style="
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center;
    "
  >
    <div class="mr-10">
      <h1>My tasks</h1>
      <p>You have {{ props.pendingTasks }} pending tasks</p>
    </div>
    <div class="text-center">
      <img :src="Logo" class="img-fluid" style="width: 150px; height: 150px" />
    </div>
  </header>
</template>