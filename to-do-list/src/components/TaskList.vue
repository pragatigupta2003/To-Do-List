<script setup>
// import { defineProps, defineEmits } from 'vue';

const props = defineProps(["tasks"]);
const emits = defineEmits(["update-task-status"]);

const emitUpdateTaskStatus = (task, completed) => {
  emits("update-task-status", { task, completed });
};

const deleteTask = (task) => {
  // Emit an event to delete the task
  emits("delete-task", task);
};
</script>

<template>
  <ul class="list-group mt-4 shadow-sm">
    <li class="list-group-item" v-for="task in props.tasks" :key="task.title">
      <div class="task-container">
        <input
          @change="(event) => emitUpdateTaskStatus(task, event.target.checked)"
          :checked="task.completed"
          :id="task.title"
          type="checkbox"
        />
        <label
          :class="{ done: task.completed }"
          :for="task.title"
          class="task-title"
        >
          {{ task.title }}
        </label>
        <label :for="task.date" class="task-date">
          {{ task.date }}
        </label>
        <button
          @click="deleteTask(task)"
          class="btn btn-danger"
          style="margin-left: 20px"
        >
          Delete
        </button>
        <!-- Delete button -->
      </div>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

.task-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}



.task-title {
  flex: 1;
  margin-right: 10px;
  margin-left: 10px;
}

.task-date {
  margin-right: 10px;
}
</style>