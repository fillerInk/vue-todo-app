<template>
  <div class="add-todo-form">
    <form @submit="addTodo">
      <input class="todo-text" v-model="title" placeholder="Enter Todo" />
      <br />
      <input type="submit" value="Submit" class="todo-button">
    </form>
  </div>
</template>

<script>
// const uuid = require('uuid')
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false
      };
      this.$emit("add-todo", newTodo);
      //to clear input once submitted
      this.title = ''
    }
  }
};
</script>

<style lang="css" scoped>
.add-todo-form {
  width: fit-content;
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
  border: 2px;
  border-style: solid;
  border-color: #333;
  border-radius: 5px;
}

.todo-text {
  font-size: large;
  width: 300px;
  height: 40px;
  margin: 10px;
}
.todo-button {
  font-size: large;
  margin: 10px;
  width: 100px;
  height: 50px;
}
</style>