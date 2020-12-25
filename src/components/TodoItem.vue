<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
        <input type="checkbox" v-on:change="$emit('change-todo', todo.id)">
        <strong class="todo-id">{{index+1}}: </strong>
        {{todo.title}}
    </span>
    <button v-on:click="$emit('remove-todo', todo.id)" class="rm">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
      todo: {
          type: Object,
          required: true
      },
      index: {
          type: Number,
          required: true
      }
  },
//   methods: {
//       changeTodo() {
//         //   this.$emit('change-todo', this.todo.id)
//           this.todo.completed = !this.todo.completed
//       }
//   }
};
</script>
<style scoped>
    li {
        display: flex;
        justify-content: space-between;
        width: 100%;
        border: 1px solid #ddd;
        margin: 5px 0;
        padding: 5px;
        box-sizing: border-box;
    }
    span {
        width: 100%;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }
    .todo-id {
        margin: 0 5px 0 5px;
    }

    .rm {
        background: rgb(236, 82, 82);
        border: none;
        border-radius: 50%;
        height: 20px;
        width: 20px;
        color: #fff;
        font-weight: bold;
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 1rem;
    }
    .done {
        text-decoration: line-through;
        opacity: 0.5;
    }
    input {
        margin-right: 0.5rem;
    }
    
</style>