<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
import Header from "./components/Header.vue";
import AddTodo from "./components/AddTodo.vue";
const axios = require("axios");

export default {
  name: "App",
  components: {
    Todos,
    Header,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(() => this.todos = this.todos.filter((todo) => todo.id !== id))
      .catch(err => console.log(err))

      
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err))
      
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
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
  margin-top: 0;
}
</style>
