<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <task
        v-for="(task, index) in tasks"
        :key="task.name"
        :task="task"
        @taskStateChanged="$emit('taskStateChanged', index)"
        @taskDeleted="$emit('taskDeleted', index)"
      />
    </template>
    <p v-else class="no-task">Sua vida está em dia :)</p>
  </div>
</template>

<script>
import Task from "./Task.vue";

export default {
  name: "TaskGrid",

  props: {
    tasks: { type: Array, required: true },
  },

  components: {
    Task,
  },
};
</script>

<style scoped>
.task-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.task-grid .task {
  margin: 10px;
}

.no-task {
  color: #aaa;
  font-size: 1.7rem;
}
</style>