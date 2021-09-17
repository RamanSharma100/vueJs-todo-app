<template>
  <div class="todosBox">
    <div v-if="todos.length < 1">
      <h1 align="center">No Todos Found</h1>
    </div>
    <div v-else>
      <Todo
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @completeTodo="completeTodo"
        @deleteTodo="deleteTodo"
      />
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  emits: ["todoComplete", "todoDelete"],
  components: {
    Todo,
  },
  props: {
    todos: {
      type: Array,
    },
  },
  methods: {
    completeTodo(value) {
      this.$emit("todoComplete", value);
    },
    deleteTodo(value) {
      this.$emit("todoDelete", value);
    },
  },
};
</script>

<style>
.todosBox {
  position: relative;
  width: 60%;
  margin: 30px auto;
}
</style>
