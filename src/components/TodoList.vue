<template>
  <div>
    <ul>
      <TodoItem
        v-for="(todo, i) in todos"
        v-bind:todo="todo"
        v-bind:index="i"
        :key="todo.id"
        @remove-todo="removeTodo"
        @change-todo="changeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  props: ["todos"],
  components: {
    TodoItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit("remove-todo", id);
    },
    changeTodo(id) {
      this.$emit("change-todo", id);
    },
  },
};
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}
</style>