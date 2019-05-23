<template>
  <div id="app">
    <h1 class="ui dividing centered header main-title">Git Bisect Example</h1>
    <div class='ui three column centered grid'>
      <div class='column' v-if="user">
        <h2 class="ui center aligned icon header">
          <i class="circular users icon"></i>
          Hi {{user.nickname || user.name}}!
        </h2>
        <h3 class="ui centered header">
          {{isUsingDefaultTasks ? 'We added automatically some tasks to start' : 'It\'s a good day to close pending tasks'}}
        </h3>
        <div class="ui divider"/>
        <todo-list v-bind:todos="todos"></todo-list>
        <create-todo v-on:create-todo="createTodo"></create-todo>
      </div>
      <first-time-ux
        @complete-ftux="saveUser"
        v-else
      />
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import TodoList from './components/TodoList';
import CreateTodo from './components/CreateTodo';
import FirstTimeUx from './components/FTUX';

export default {
  name: 'app',
  components: {
    TodoList,
    CreateTodo,
    FirstTimeUx,
  },
  data() {
    const tasksStr = localStorage.getItem('tasks');
    const userStr = localStorage.getItem('user');
    const todos = tasksStr ? JSON.parse(tasksStr) : this.getDefaultTasks();

    localStorage.setItem('tasks', JSON.stringify(todos));
    return {
      todos,
      user: userStr && JSON.parse(userStr),
      isUsingDefaultTasks: !tasksStr,
    };
  },
  watch: {
    todos(val) {
      localStorage.setItem('tasks', JSON.stringify(val));
    },
  },
  methods: {
    saveUser(user) {
      this.user = user;
      localStorage.setItem('user', JSON.stringify(user));
    },
    createTodo(newTodo) {
      this.todos.push(newTodo);
      sweetalert('Success!', 'To-Do created!', 'success');
    },
    getDefaultTasks() {
      const today = new Date();
      const yesterday = new Date();
      const tomorrow = new Date();

      tomorrow.setDate(today.getDate() + 1);
      yesterday.setDate(today.getDate() - 1);

      return [{
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
      }];
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
