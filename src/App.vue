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
      }, {
        title: 'Go to exercise-1 branch',
        project: 'Git Bisect Workshop',
        created: yesterday,
        due: tomorrow,
        done: false,
        id: 2,
      }, {
        title: 'Find the commit when the bug was injected',
        project: 'Git Bisect Workshop: Exercise 1',
        created: yesterday,
        due: tomorrow,
        done: false,
        id: 3,
      }, {
        title: 'Go to exercise-2 branch',
        project: 'Git Bisect Workshop',
        created: yesterday,
        due: tomorrow,
        done: false,
        id: 4,
      }, {
        title: 'Find the commit when the bug was injected',
        project: 'Git Bisect Workshop: Exercise 2',
        created: yesterday,
        due: tomorrow,
        done: false,
        id: 5,
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
    margin-bottom: 3rem;
  }
</style>
