<template>
  <div id="app">
    <h1 class="ui dividing centered header main-title">Git Bisect Example</h1>
    <div class='ui two column centered grid'>
      <div class='column'>
        <todo-list v-bind:todos="todos"></todo-list>
        <create-todo v-on:create-todo="createTodo"></create-todo>
      </div>
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import TodoList from './components/TodoList';
import CreateTodo from './components/CreateTodo';

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo,
  },
  data() {
    const today = new Date();
    const yesterday = new Date();
    const tomorrow = new Date();

    tomorrow.setDate(today.getDate() + 1);
    yesterday.setDate(today.getDate() - 1);
    return {
      todos: [{
        title: 'Clone the repo',
        project: 'Git Bisect Workshop',
        created: yesterday,
        due: tomorrow,
        done: true,
        completed: today,
        id: 1,
        deleted: false,
      }, {
        title: 'Go to exercise-1 branch',
        project: 'Git Bisect Workshop',
        created: yesterday,
        due: tomorrow,
        done: false,
        completed: null,
        id: 2,
        deleted: false,
      }, {
        title: 'Find the commit when the bug was injected',
        project: 'Git Bisect Workshop: Exercise 1',
        created: yesterday,
        due: tomorrow,
        done: false,
        completed: null,
        id: 3,
        deleted: false,
      }, {
        title: 'Go to exercise-2 branch',
        project: 'Git Bisect Workshop',
        created: yesterday,
        due: tomorrow,
        done: false,
        completed: null,
        id: 4,
        deleted: false,
      }, {
        title: 'Find the commit when the bug was injected',
        project: 'Git Bisect Workshop: Exercise 2',
        created: yesterday,
        due: tomorrow,
        done: false,
        completed: null,
        id: 5,
        deleted: false,
      }],
    };
  },
  methods: {
    createTodo(newTodo) {
      this.todos.push(newTodo);
      sweetalert('Success!', 'To-Do created!', 'success');
    },
  },
};
</script>

<style scoped>
  h1.main-title {
    padding: 3rem;
    background-color: #21BA45;
    color: white;
    margin-bottom: 3rem;
  }
</style>
