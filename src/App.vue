<template>
  <div id="app">
    <Header/>
    <Todos v-bind:todos="todos" v-on:delTodo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "./components/Todos";
import Header from "./components/layout/Header";

export default {
  name: "app",
  components: {
    Todos,
    Header
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo One",
          completed: false
        },
        {
          id: 2,
          title: "Todo Two",
          completed: true
        },
        {
          id: 3,
          title: "Todo Three",
          completed: false
        }
      ]
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id); // reassignment
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
