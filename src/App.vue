<template>
  <div>
    <todo-list v-bind:todos="todos"></todo-list>
    <create-todo v-on:create-todo="addTodo"></create-todo>
  </div>
</template>

<script>
  import TodoList from './components/TodoList';
  import CreateTodo from './components/CreateTodo';
  // import axios from 'axios';

  export default {
    name: 'app',
    components: {
      TodoList,
      CreateTodo,
    },
    created() {
      const request = new Request('http://localhost:3001/tasks', { method: 'GET' });
      fetch(request).then(resp => resp.json()).then((data) => {
        this.todos = data;
      });
    },
    // data function avails data to the template
    data() {
      return {
        todos: [],
      };
    },
    methods: {
      addTodo(todo) {
        this.todos.push(todo);
      },
    },
  };

</script>


<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>




