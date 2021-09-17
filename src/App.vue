<template>
  <Heading name="Vue Js Todo App" />
  <Form @addTodo="addTodo" :todos="todos" />
  <Todos :todos="todos" @todoComplete="todoComplete" @todoDelete="todoDelete" />
</template>

<script>
import Heading from "./components/Heading.vue";
import Form from "./components/Form.vue";
import Todos from "./components/Todos.vue";

export default {
  name: "App",
  components: {
    Heading,
    Form,
    Todos,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          text: "Star this repo",
          completed: false,
        },
        {
          id: 2,
          text: "Completed Project",
          completed: true,
        },
      ],
    };
  },
  methods: {
    addTodo($event) {
      this.todos.push($event);
    },
    todoComplete(value) {
      const currentTodo = this.todos.find((tdo) => tdo.id === value);
      currentTodo.completed = true;
      this.todos = this.todos.map((tdo) =>
        tdo.id === value ? currentTodo : tdo
      );
    },
    todoDelete(value) {
      this.todos = this.todos.filter((tdo) => tdo.id !== value);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
