<template>
  <div id="app">
    <Addtodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>


<script>
import Todos from "../components/Todos";
import Addtodo from "../components/AddTodo";
import axios from "axios";
export default {
  name: "Home",
  components: {
    Todos,
    Addtodo
  },
  data() {
    return {
      todos: [
        // {
        //   id: 1,
        //   title: "Todo One",
        //   completed: false
        // },
        // {
        //   id: 2,
        //   title: "Todo Two",
        //   completed: true
        // },
        // {
        //   id: 3,
        //   title: "Todo Three",
        //   completed: false
        // }
        /////////////////////////////////////////////////
      ]
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then
        // res => (this.todos = this.todos.filter(todo => todo.id !== id))   //this one doesnt work with the delte function
        ()

        .catch(err => console.log(err));
      console.log(id);

      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title, //es6 title: title
          completed //es6 too
        })
        .then(res => (this.todos = this.todos = [...this.todos, res.data]))
        .catch(err => console.log(err));
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, san-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>