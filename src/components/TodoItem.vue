<template>
  <div class="todoitem" v-bind:class="{'is-complete-card':todo.completed}">
    <input id="inputRadio" value="done" type="checkbox" v-on:change="markComplete" />
    <h3 v-bind:class="{'is-complete':todo.completed}">{{todo.title}}</h3>
    <button @click="$emit('del-todo',todo.id)" class="del">X</button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      if (this.todo.completed == false) {
        this.todo.completed = true;
      } else {
        this.todo.completed = false;
      }
    }
  }
};
</script>

<style lang="css" scoped>
.todoitem {
  border: 2px;
  border-radius: 10px;
  border-color: #333;
  background-color: rgb(118, 202, 167);
  width: 400px;
  height: 100px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 10px;
  padding: 10px;
  padding-left: 30px;
  text-align: left;
  display: flex;
}

.is-complete-card {
  background-color: #555;
}

.is-complete {
  background-color: #555;
  color: #fff;
  text-decoration: line-through;
}

.del {
  background-color: red;
  color: #fff;
  height: 30px;
  margin-left: auto;
  margin-right: 0;
}
</style>