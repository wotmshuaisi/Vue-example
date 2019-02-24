<template>
  <div id="app">
    <AddTodo v-on:addTodo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:delTodo="deleteTodo"/>
  </div>
</template>

<script>
/* eslint-disable no-console */

import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
          this.todos = this.todos.filter(todo => todo.id !== id); // reassignment
        })
        .catch(err => {
          console.log(err);
        });
    },
    addTodo(todo) {
      const { title, completed } = todo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => {
          this.todos.push(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=8")
      .then(res => {
        this.todos = res.data;
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>

<style lang="less">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

btn:hover {
  background: #666;
}
</style>
