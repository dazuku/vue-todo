<template>
  <div>
    <div class="ui two column divided grid">
      <div class="column">
        <p class="tasks tasks--completed">Completed Tasks: {{completedTodos.length}}</p>
        <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in completedTodos" :key="todo.id" :todo.sync="todo" />
      </div>
      <div class="column">
        <p class="tasks tasks--pending">Pending Tasks: {{pendingTodos.length}}</p>
        <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in pendingTodos" :key="todo.id" :todo.sync="todo" />
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
      return this.todos.filter(todo => todo.done);
    },
    pendingTodos() {
      return this.todos.filter(todo => !todo.done);
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
        this.todos.splice(todoIndex, 1);
        sweetalert('Deleted!', 'Your To-Do has been deleted.', 'success');
      });
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
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
</style>

