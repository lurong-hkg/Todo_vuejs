<template>
  <div class='ui centered card'>
    // Todo shown when we are not in editing mode.
    <div class="content" v-show="!isEditing">
      <div class='header'>
        {{ todo.name }}
      </div>
      <div class='meta'>
        {{ todo.name }}
      </div>
      <div class='extra content'>
          <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' v-on:click="deleteTodo">
       <i class='trash icon'></i>
       </span>
      </div>
    </div>
    // form is visible when we are in editing mode
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.name">
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="todo.name">
        </div>
        <div class="field">
          <input type="radio" value="pending" v-model="todo.status[0]">
          <label>Pending</label>
          <br>
          <input type="radio" value="completed" v-model="todo.status[0]">
          <label>Completed</label>
          <br>
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
    <div :class="statusClassBindings" class="ui bottom attached basic button" v-show="!isEditing" @click="toggleCompleteStaus">
      {{todo.status[0]}}
    </div>
  </div>
</template>

<script>
  export default {
    props: ['todo'],
    data() {
      return {
        isEditing: false,
      };
    },
    computed: {
      statusClassBindings: function () {
        return {
          red: this.todo.status[0] === 'pending',
          green: this.todo.status[0] === 'completed',
        };
      },
    },
    methods: {
      showForm() {
        this.isEditing = true;
      },
      hideForm() {
        this.isEditing = false;
      },
      deleteTodo() {
        this.$emit('delete-todo', this.todo);
      },
      toggleCompleteStaus() {
        this.$emit('toggle-todo', this.todo);
      },
    },
  };
</script>
