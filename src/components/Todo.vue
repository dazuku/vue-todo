<template>
  <div class='ui centered card' :class="todo.done ? 'todo--completed' : 'todo--pending'">
    <div class="content" v-show="!isEditing">
      <div class='header'>
          {{ todo.title }}
      </div>
      <div class='meta'>
        <div>{{ todo.project }}</div>
        <div>Created Date: {{ created }}</div>
        <div v-if="!todo.done">Due Date: {{ due }}</div>
        <div v-else>Completed Date: {{ completed }}</div>
      </div>
      <div class='extra content'>
          <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
          <i class='trash icon'></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="todo.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
    <div class="custom-button">
      <div class='ui bottom attached green basic button' v-show="!isEditing &&todo.done" disabled>
          Completed
      </div>
      <div class='ui bottom attached red basic button' v-on:click="completeTodo(todo)" v-show="!isEditing && !todo.done">
          Pending
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  import moment from 'moment';

  export default {
    props: ['todo'],
    data() {
      return {
        isEditing: false,
      };
    },
    computed: {
      created() {
        return moment(this.todo.created).format('LL');
      },
      due() {
        return moment(this.todo.due).format('LL');
      },
      completed() {
        return this.todo.created && moment(this.todo.completed).format('LL');
      },
    },
    methods: {
      completeTodo(todo) {
        this.$emit('complete-todo', todo);
      },
      deleteTodo(todo) {
        this.$emit('delete-todo', todo);
      },
      showForm() {
        this.isEditing = true;
      },
      hideForm() {
        this.isEditing = false;
      },
    },
  };
</script>

<style scoped>
  .todo--completed {
    border: #21BA45 solid 1px;
  }
  .todo--pending {
    border: #DB2828 solid 1px;
  }
  .custom-button {
    background-color: white;
    padding: 1rem;
  }
</style>
