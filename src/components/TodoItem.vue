<template>
  <ul class="todo-item" v-bind:class="{'is-completed':todo.completed}">
    <li>
      <input type="checkbox" :checked="todo.completed" v-on:change="markComplete()">
      {{todo.title}}
      <button @click="$emit('delTodo', todo.id)" class="del">X</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete(todoId) {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style lang="less" scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-completed {
  text-decoration: line-through;
}

.del {
  background: red;
  color: white;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
  border: 1px solid gray;
}
</style>
