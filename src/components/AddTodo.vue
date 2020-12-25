<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" />
    <button type="submit">Add</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      dateIdDefault: "without date"
    };
  },
  props: ['dateID'],
  methods: {
    onSubmit() {
      if(this.title.trim()) {
        const newTodo = {
          id: Date.now(),
          title: this.title,
          dateID: '',
          completed: false,
          dateID: this.dateID ? this.dateID : this.dateIdDefault
        }
        this.$emit('add-todo', newTodo)
        this.title = ''
      }
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}
input {
  width: 90%;
  max-width: 400px;
  margin-right: 0.5rem;
  padding: 0.3rem;
}
button {
  width: 100px;
  padding: 0.3rem;
}
</style>