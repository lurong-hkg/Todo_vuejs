<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <label>Title</label>
            <input v-model="titleText" type='text' ref='title' defaultValue="">
          </div>
          <div class='field'>
            <label>Project</label>
            <input type='text' v-model='projectText' defaultValue="">
          </div>
          <div class="field">
            <input type="radio" value="PENDING" v-model='done'>
            <label>pending</label>
            <br>
            <input type="radio" value="DONE"  v-model='done'>
            <label>Completed</label>
            <br>
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' v-on:click="sendForm">
              Create
            </button>
            <button class='ui basic red button' v-on:click="closeForm">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        titleText: '',
        projectText: '',
        done: null,
        isCreating: false,
      };
    },
    methods: {
      openForm() {
        this.isCreating = true;
      },
      closeForm() {
        this.isCreating = false;
      },
      sendForm() {
        if (this.titleText.length > 0 && this.projectText.length > 0) {
          const title = this.titleText;
          const project = this.projectText;
          const done = this.done;
          this.$emit('create-todo', {
            title,
            project,
            done,
          });
          this.newTodoText = '';
        }
        this.isCreating = false;
      },
    },
  };
</script>
