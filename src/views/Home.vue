<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todoItemsen="todos" v-on:del-todoItem="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo
  },
  //Säger att appen ska ha 3 default todos.
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      fetch('https://jsonplaceholder.typicode.com/todos/' + id, {
        method: 'DELETE',
      })
      .then(response => response.json()) // or res.json()
      .then((data) => {
        console.log(data);
        this.todos = this.todos.filter(todoItem => todoItem.id !== id)
      })
      .catch(err => console.log(err));
      
    },
    addTodo(newTodo) {
      //[...] betyder att man fyller den nya arrayen med samma sak, plus 1 sak till.
      const { title, completed } = newTodo;
      console.log( title, completed);
      fetch('https://jsonplaceholder.typicode.com/todos', {
        method: 'POST', // or 'PUT'
        headers: {
          'Content-Type': 'application/json',
        },
       body: JSON.stringify({
          title,
          completed
        })
      })
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        this.todos = [...this.todos, data];
      })
      .catch((error) => {
      console.error('Error:', error);
    });
    }
  },
  created() {
    //https://jsonplaceholder.typicode.com/todos/
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(response => {
        return response.json();
      })
      .then(data => {
        this.todos = data;
        console.log(data);
      });
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
  font-family: Arial, Arial, Helvetica, sans-serif;
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

