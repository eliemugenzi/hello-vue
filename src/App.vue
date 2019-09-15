<template>
  <div id="app">
    <Header />
    <p>{{msg}}</p>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:delete-todo="deleteTodo" />
  </div>
</template>

<script>
import axios from "axios";
import Todos from "./components/Todos";
import Header from "./components/layouts/Header";
import AddTodo from "./components/AddTodo";

export default {
  name: "app",
  components: {
    Todos,
    Header,
    AddTodo
  },
  data: () => {
    return {
      msg: "Hello",
      todos: []
    };
  },
  methods: {
    async deleteTodo(id) {
      try {
        const { data: response } = await axios.delete(
          `https://jsonplaceholder.typicode.com/todos/${id}`
        );
        this.todos = this.todos.filter(todo => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    },
    async addTodo(newTodo) {
      const { title, completed } = newTodo;
      try {
        const { data: response } = await axios.post(
          "https://jsonplaceholder.typicode.com/todos",
          {
            title,
            completed
          }
        );
        this.todos = [response, ...this.todos];
      } catch (error) {
        console.log(error);
      }
    }
  },
  async created() {
    try {
      const { data: response } = await axios.get(
        "https://jsonplaceholder.typicode.com/todos?_limit=10"
      );
      this.todos = response;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
