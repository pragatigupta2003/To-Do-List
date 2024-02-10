<script setup>
const props = defineProps([
  "addTask",
  "tempTask",
  "changeFilter",
  "editTempTask",
]);
</script>

<template>
  <form @submit.prevent="props.addTask">
    <div class="row">
      <div class="col">
        <input
          :value="props.tempTask"
          @change="props.editTempTask"
          required
          type="text"
          placeholder="Enter the task description here"
          class="form-control shadow-sm"
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary shadow-sm">
          Add Task
        </button>
      </div>
      <div class="col-md-2">
        <select @change="props.changeFilter" class="form-control shadow-sm">
          <option value="all">All tasks</option>
          <option value="pending">Pending</option>
          <option value="completed">Completed</option>
        </select>
      </div>
    </div>
  </form>
</template>