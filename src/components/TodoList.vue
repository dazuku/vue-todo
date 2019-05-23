<template>
  <div>
    <div class="ui three column divided grid">
      <div class="column">
        <p class="tasks tasks--completed">Completed Tasks: {{completedTodos.length}}</p>
        <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in completedTodos" :key="todo.id" :todo.sync="todo" />
      </div>
      <div class="column">
        <p class="tasks tasks--pending">Pending Tasks: {{pendingTodos.length}}</p>
        <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in pendingTodos" :key="todo.id" :todo.sync="todo" />
      </div>
      <div class="column">
        <p class="tasks tasks--deleted">Deleted Tasks: {{deletedTodos.length}}</p>
        <todo
          v-on:recover-todo="recoverTodo"
          v-on:delete-todo="deleteTodo"
          v-on:complete-todo="completeTodo"
          v-for="todo in deletedTodos"
          :key="todo.id"
          :todo.sync="todo"
        />
      </div>
    </div>
  </div>
</template>

<script type = "text/javascript" >
import sweetalert from 'sweetalert';
import Todo from './Todo';

export default {
  props: ['todos'],
  components: {
    Todo,
  },
  computed: {
    completedTodos() {
      return this.todos.filter(todo => todo.done && !todo.deleted);
    },
    pendingTodos() {
      return this.todos.filter(todo => !todo.done && !todo.deleted);
    },
    deletedTodos() {
      return this.todos.filter(todo => todo.deleted);
    },
  },
  methods: {
    deleteTodo(todo) {
      sweetalert({
        title: 'Are you sure?',
        text: 'This To-Do will be permanently deleted!',
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#DD6B55',
        confirmButtonText: 'Yes, delete it!',
        closeOnConfirm: false,
      },
      () => {
        const todoIndex = this.todos.indexOf(todo);
        this.todos[todoIndex].deleted = true;
        // this.todos.splice(todoIndex, 1);
        sweetalert('Deleted!', 'Your To-Do has been deleted.', 'success');
      });
    },
    recoverTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].deleted = false;
      sweetalert('Success!', 'To-Do recovered!', 'success');
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      this.todos[todoIndex].completed = new Date();
      sweetalert('Success!', 'To-Do completed!', 'success');
    },
  },
};
</script>

<style scoped>
p.tasks {
  font-size: 2rem;
}
p.tasks--completed {
  color: #21BA45;
}
p.tasks--pending {
  color: #DB2828;
}
p.tasks--deleted {
  color: #AAA;
}
</style>

