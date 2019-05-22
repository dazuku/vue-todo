<template>
  <div id="app">
    <h1 class="ui dividing centered header">Git Bisect example</h1>
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
      this.todos.push(newTodo);
      sweetalert('Success!', 'To-Do created!', 'success');
    },
  },
};
</script>
