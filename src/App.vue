<template>
  <div id="app">
    <h1 class="ui dividing centered header main-title">Git Bisect Example</h1>
    <div class='ui three column centered grid'>
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
    return {
      todos: [{
        title: 'Clone the repo',
        project: 'Git Bisect Workshop',
        done: true,
      }, {
        title: 'Go to exercise-1 branch',
        project: 'Git Bisect Workshop',
        done: false,
      }, {
        title: 'Find the commit when the bug was injected',
        project: 'Git Bisect Workshop: Exercise 1',
        done: false,
      }, {
        title: 'Go to exercise-2 branch',
        project: 'Git Bisect Workshop',
        done: false,
      }, {
        title: 'Find the commit when the bug was injected',
        project: 'Git Bisect Workshop: Exercise 2',
        done: false,
      }],
    };
  },
  methods: {
    createTodo(newTodo) {
      console.log('new Todo', newTodo);
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
  }
</style>
