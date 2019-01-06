<template>
  <div class="container">
    <h1>Todo List</h1>

    <div>
      <form @submit.prevent="addTodo">
        <input class="todo-input" type="text" placeholder="Enter a new Task" v-model="task">
      </form>
    </div>
    <div id="app">
      <ul class="tasks">
        <li
          v-for="todo in todos"
          :class="{completed: todo.completed}"
          class="task"
          :key="todo.id"
          @click="toggleTodo(todo.id)"
          @dblclick="deleteTodo(todo.id)"
        >{{todo.task}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      newId: 3
    };
  },
  computed: {
    todos() {
      return this.$store.getters.getTodos;
    }
  },
  methods: {
    toggleTodo: function(id) {
      this.$store.dispatch("toggleTodo", id);
    },
    deleteTodo: function(id) {
      this.$store.dispatch("deleteTodo", id);
    },
    addTodo: function() {
      this.$store.dispatch("addTodo", this);
      this.newId++;
      this.task = "";
    }
  }
};
</script>

<style>
html {
  font-family: sans-serif;
  background: linear-gradient(45deg, #6cfd9f, #6887ff);
  height: 100%;
  color: #333;
}
body {
  display: flex;
  height: 100%;
  margin: 0;
}
.container {
  width: 24rem;
  margin: auto;
  background-color: white;
  border-radius: 0.5rem;
  padding: 1rem;
  box-shadow: 0 0 2rem rgba(0, 0, 0, 0.25);
}
h1 {
  text-align: center;
  margin-top: 0;
}
.todo-input {
  width: 100%;
  padding: 0.5rem;
  font-size: 1rem;
  outline: none;
  border-radius: 0.25rem;
  border-style: none;
  border: solid 1px lightgray;
  box-sizing: border-box;
}
.tasks {
  padding-left: 1.5rem;
}
.task {
  margin-bottom: 0.5rem;
}
.task:hover {
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
  color: #555;
}
</style>
