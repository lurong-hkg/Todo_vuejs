<template>
  <div>
    <todo v-for="todo in todos" v-bind:todo="todo" :key="todo.id" v-on:delete-todo="deleteTodo"
          v-on:toggle-todo="toggleCompleteStaus">
    </todo>

  </div>
</template>

<script type="text/javascript">

  import Vue from 'vue';
  import Todo from './Todo';

  export default {
    name: 'TodoList',
    props: ['todos'],
    components: {
      Todo,
    },
    methods: {
      deleteTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
      },
      toggleCompleteStaus(todo) {
        const todoIndex = this.todos.indexOf(todo);
        if (todo.status[0] === 'pending') {
          Vue.set(this.todos[todoIndex].status, 0, 'completed');
        } else {
          Vue.set(this.todos[todoIndex].status, 0, 'pending');
        }
      },
    },
  };

</script>
