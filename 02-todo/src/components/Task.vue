<template>
  <div
    class="task"
    :class="stateClass"
    @click="$emit('taskStateChanged', task)"
  >
    <span @click.stop="$emit('taskDeleted', task)" class="close">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  name: "Task",

  props: {
    task: { type: Object, required: true },
  },

  computed: {
    stateClass() {
      return {
        pending: this.task.pending,
        done: !this.task.pending,
      };
    },
  },
};
</script>

<style scoped>
.task {
  position: relative;
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  padding: 10px;
  border-radius: 8px;
  font-size: 2rem;
  font-weight: 300;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.pending {
  border-left: 12px solid #9e2a20;
  background-color: #db3a2c;
}

.done {
  color: #ddd;
  border-left: 12px solid #0a773b;
  background-color: #04d361;
  text-decoration: line-through;
}

.pending .close {
  background-color: #9e2a20;
}

.done .close {
  background-color: #0a773b;
}

.close {
  position: absolute;
  right: 10px;
  top: 10px;
  font-size: 0.9rem;
  font-weight: 600;
  height: 20px;
  width: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
}
</style>