<template>
  <div>
    <div class="ui one column divided grid">
      </div>
        <div class="column">
        <div class="dropdown-container">
          <div class="ui dropdown" @click="toggleDropdown">
            <div class="text">{{selectedStep.title}}</div>
            <i class="dropdown icon"></i>
            <div class="menu" :style="{ display: showDropdown ? 'block' : 'none' }">
              <div
                class="item"
                v-for="(step, index) in config"
                :key="index"
                @click.stop="selectStep(index)"
              >
                {{step.title}}
              </div>
            </div>
          </div>
        </div>
        <p class="tasks" :class="selectedStep.class">{{selectedStep.title}}: {{selectedTodos.length}}</p>
        <todo
          v-on:recover-todo="recoverTodo"
          v-on:delete-todo="deleteTodo"
          v-on:complete-todo="completeTodo"
          v-for="todo in selectedTodos"
          :type.sync="selectedStep.type"
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
  data() {
    return {
      showDropdown: false,
      selectedIndex: 0,
      steps: [
        'completedTodos',
        'pendingTodos',
        'deletedTodos',
      ],
      config: [
        {
          title: 'Completed Tasks',
          class: 'tasks--completed',
          field: 'completedTodos',
          type: 'completed',
        },
        {
          title: 'Pending Tasks',
          class: 'tasks--pending',
          field: 'pendingTodos',
          type: 'pending',
        },
        {
          title: 'Deleted Tasks',
          class: 'tasks--deleted',
          field: 'completedTodos',
          type: 'deleted',
        },
        {
          title: 'Show all',
          class: 'tasks--all',
          field: 'todos',
          type: 'all',
        },
      ],
    };
  },
  computed: {
    selectedStep() {
      return this.config[this.selectedIndex];
    },
    selectedTodos() {
      return this[this.selectedStep.field];
    },
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
    toggleDropdown() {
      this.showDropdown = true;
    },
    selectStep(index) {
      this.selectedIndex = index;
      this.showDropdown = false;
    },
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
  text-align: center;
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
.dropdown-container {
  display: flex;
  justify-content: center;
  padding: 1rem;
}
</style>

