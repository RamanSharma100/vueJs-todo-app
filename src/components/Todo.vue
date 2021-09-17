<template>
  <div class="todo">
    <div class="left">
      <input
        type="checkbox"
        :checked="todo.completed"
        :disabled="todo.completed"
        @click="completeTodo"
      />
      <h2>{{ todo.text }}</h2>
    </div>
    <button type="button" v-if="todo.completed" @click="deleteTodo">
      Delete
    </button>
  </div>
</template>

<script>
export default {
  emits: ["completeTodo", "deleteTodo"],
  props: {
    todo: {
      type: Object,
    },
  },
  methods: {
    completeTodo() {
      this.$emit("completeTodo", this.todo.id);
    },
    deleteTodo() {
      this.$emit("deleteTodo", this.todo.id);
    },
  },
};
</script>

<style>
.todo {
  display: grid;
  grid-template-columns: 80% auto;
  padding: 0px 15px;
  border-bottom: 0.5px solid rgb(185, 185, 185);
}
.todo .left {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.todo .left input {
  height: 25px;
  width: 25px;
  margin-right: 20px;
}
.todo button {
  height: 40px;
  margin-top: 15px;
  cursor: pointer;
  margin-right: -10px;
  margin-left: 10px;
  background: rgba(182, 9, 9, 0.89);
  border: 1px solid rgba(182, 9, 9, 0.89);
  color: #fff;
}
</style>
