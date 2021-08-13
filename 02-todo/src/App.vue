<template>
  <div id="app">
    <h1>Tarefas</h1>
    <tasks-progress :progress="progress" />
    <new-task @taskAdded="addTask" />
    <task-grid
      :tasks="tasks"
      @taskStateChanged="toggleTaskState"
      @taskDeleted="deleteTask"
    />
  </div>
</template>

<script>
import TasksProgress from "./components/TasksProgress.vue";
import NewTask from "./components/NewTask.vue";
import TaskGrid from "./components/TaskGrid.vue";

export default {
  name: "App",

  components: {
    TasksProgress,
    NewTask,
    TaskGrid,
  },

  data() {
    return {
      tasks: [],
    };
  },

  computed: {
    progress() {
      const total = this.tasks.length;
      const done = this.tasks.filter((t) => !t.pending).length;
      return Math.round((done / total) * 100) || 0;
    },
  },

  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem("tasks", JSON.stringify(this.tasks));
      },
    },
  },

  methods: {
    addTask(task) {
      const sameName = (t) => t.name === task.name;
      const reallyNew = this.tasks.filter(sameName).length == 0;

      if (reallyNew) {
        this.tasks.push({
          name: task.name,
          pending: task.pending || true,
        });
      }
    },

    toggleTaskState(index) {
      this.tasks[index].pending = !this.tasks[index].pending;
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },

  created() {
    const json = localStorage.getItem("tasks");
    this.tasks = JSON.parse(json) || [];
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  font-family: "Lato", sans-serif;
  background: #201f24;
  color: #fff;
}

#app {
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#app h1 {
  margin-bottom: 15px;
  font-weight: 300;
  font-size: 3rem;
}
</style>
