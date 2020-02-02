<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import Header from "../components/layout/Header";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "app",
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
      // todos: [
      //   {
      //     id: 1,
      //     title: "Todo One",
      //     completed: false
      //   },
      //   {
      //     id: 2,
      //     title: "Todo Two",
      //     completed: false
      //   },
      //   {
      //     id: 3,
      //     title: "Todo Three",
      //     completed: false
      //   }
      // ]
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(item => item.id !== id);
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => {
        this.todos = res.data;
      })
      .catch(error => console.log(error));
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
  margin-top: 6px;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px, 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
