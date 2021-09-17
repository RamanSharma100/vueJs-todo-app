<template>
  <div class="error">
    {{ error }}
  </div>
  <div class="formDiv">
    <form class="form" @submit.prevent="handleSubmit">
      <input type="text" v-model="todo" placeholder="Add Todo" />
      <button type="submit">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  emits: ["addTodo"],
  props: {
    todos: { type: Array },
  },
  data() {
    return {
      todo: "",
      error: "",
    };
  },
  methods: {
    handleSubmit() {
      this.validateInput();
      if (!this.error) {
        const newTodo = {
          id:
            this.todos.length > 0
              ? this.todos[this.todos.length - 1].id + 1
              : 1,
          completed: false,
          text: this.todo,
        };

        this.$emit("addTodo", newTodo);
        this.todo = "";
      }
    },
    validateInput() {
      if (!this.todo) {
        this.error = "Please fill in all fields";
      } else {
        this.error = "";
      }
    },
  },
};
</script>

<style>
div.formDiv {
  position: relative;
  height: 35px;
  width: 60%;
  margin: 100px auto;
}
.error {
  color: red;
}
.form {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.form input {
  height: 100%;
  width: 80%;
  padding: 0px 15px;
  box-shadow: none;
  outline: none;
  border-right: 0;
  border-top: 0;
  border-left: 0;
}
.form input:focus {
  border-color: #017bf5;
  border-right: 0;
}
.form button {
  width: 19%;
  height: 100%;
  border-color: #000;
  background: #000;
  color: #fff;
  cursor: pointer;
}
</style>
