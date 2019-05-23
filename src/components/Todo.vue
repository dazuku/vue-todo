<template>
  <div class='ui centered card' :class="cardClass">
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
        <span v-if="!todo.deleted" class='right floated trash icon' v-on:click="deleteTodo(todo)">
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
        <div class='field'>
          <label>Due Date</label>
          <input type='date' v-model="todo.due" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
    <div class="custom-button">
      <div class='ui bottom attached green basic button' v-if="!isEditing && type === 'completed'" disabled>
          Completed
      </div>
      <div class='ui bottom attached red basic button' v-on:click="completeTodo(todo)" v-if="!isEditing && type === 'pending'">
          Pending
      </div>
      <div class='ui bottom attached gray basic button' v-on:click="recoverTodo(todo)" v-if="!isEditing && type === 'deleted'">
          Recover
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
  import moment from 'moment';

  export default {
    props: ['todo', 'type'],
    data() {
      return {
        isEditing: false,
        types: {
          completed: 'todo--completed',
          pending: 'todo--pending',
          deleted: 'todo--deleted',
        },
      };
    },
    computed: {
      cardClass() {
        return this.types[this.type];
      },
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
      recoverTodo(todo) {
        this.$emit('recover-todo', todo);
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
  .todo--deleted {
    border: #aaa solid 1px;
  }
  .custom-button {
    background-color: white;
    padding: 1rem;
  }
</style>
