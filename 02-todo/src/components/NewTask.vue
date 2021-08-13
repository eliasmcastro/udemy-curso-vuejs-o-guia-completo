<template>
  <div class="new-task">
    <input
      type="text"
      class="form-element"
      placeholder="Nova tarefa?"
      v-model="name"
      @keydown.enter="add"
    />
    <button class="form-element" @click="add" title="Adicionar">+</button>
  </div>
</template>

<script>
export default {
  name: "NewTask",

  data() {
    return {
      name: "",
    };
  },

  methods: {
    add() {
      if (this.name != "") {
        this.$emit("taskAdded", { name: this.name });
        this.name = "";
      }
    },
  },
};
</script>

<style scoped>
.new-task {
  margin: 35px;
}

.form-element {
  outline: none;
  font-size: 2rem;
  border: 1px solid #fff;
  padding: 5px 10px 8px;
  color: #fff;
}

input.form-element {
  max-width: 500px;
  background: #121214;
  border: solid 2px #121214;
  border-right: none;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

input.form-element:focus {
  border: solid 2px #8257e6;
  border-right: none;
}

button.form-element {
  border-left: none;
  background-color: #8257e5;
  border: solid 2px #8257e5;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  cursor: pointer;
}

button.form-element:hover {
  background-color: #a883ff;
  border: solid 2px #a883ff;
}
</style>