<template>
  <div class="tasks-progress">
    <span class="progress-value">{{ progress }}%</span>
    <div class="progress-bar" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<script>
export default {
  name: "TasksProgress",

  props: {
    progress: { type: Number, default: 0 },
  },
};
</script>

<style scoped>
.tasks-progress {
  margin: 15px;
  position: relative;
  width: 80%;
  border: solid 1px #fff;
  color: #fff;
  border-radius: 8px;
  margin-bottom: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.progress-bar {
  position: absolute;
  border-radius: 8px;
  height: 100%;
  background-color: #04d361;
  align-self: flex-start;
}

.progress-value {
  z-index: 1;
  font-size: 1.5rem;
}
</style>