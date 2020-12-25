<template>
  <div class="app">
    <h1>Todo App</h1>
    <div class="wrapper">
      <Calendar @add-date="addDate" />
      <div>
        <AddTodo @add-todo="addTodo" v-bind:dateID="dateID" />
        <TodoList
          v-if="filteredByDate.length"
          v-bind:todos="filteredByDate"
          v-bind:dateID="dateID"
          @change-todo="changeTodo"
          @remove-todo="removeTodo"
        />
        <p v-else>No todos!</p>
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo";
import Calendar from "@/components/Calendar";

export default {
  name: "App",
  data() {
    return {
      todos: localStorage.getItem("todos")
        ? JSON.parse(localStorage.getItem("todos"))
        : [],
      dateID: `${new Date().getDate()}/${new Date().getMonth()+1}/${new Date().getFullYear()}`
    };
  },
  mounted() {
    localStorage.setItem("todos", JSON.stringify(this.todos));
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  methods: {
    removeTodo(id) {
      let newTodoArray = this.todos.filter((todo) => todo.id !== id);
      localStorage.setItem("todos", JSON.stringify(newTodoArray));
      this.todos = JSON.parse(localStorage.getItem("todos"));
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.todos = JSON.parse(localStorage.getItem("todos"));
    },
    changeTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
          localStorage.setItem("todos", JSON.stringify(this.todos));
        }
      });
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    addDate(value) {
      this.dateID = value;
    }
  },
  computed: {
    filteredByDate() {
      if (this.dateID !== "without date") {
        return this.todos.filter((todo) => todo.dateID === this.dateID);
      } else {
        return this.todos;
      }
    },
  },
  components: {
    TodoList,
    AddTodo,
    Calendar,
  },
};
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 100%;
}
.wrapper {
  display: flex;
  justify-content: center;
  width: 100%;
  margin: 0 auto;
}
</style>
