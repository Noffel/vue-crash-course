<template>
  <div id="app">

  <AddTodo v-on:add-todo="addTodo" />
  <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />

  </div>

</template>




<script>

import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios'; //install axios - it is an HTTP library to make GET, POST, etc. requests


export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },

// This is where we will store all the data

  data() {
    return{
      todos: []
      
    }
  },

  methods: {
    deleteTodo(id) 
    {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`) // Use back-ticks to put variable in the URL 
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err));



      this.todos = this.todos.filter(todo => todo.id !== id);
    },

    addTodo(newTodo) {
      const{ title, completed } = newTodo;
      
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })

      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err));

      
      
    }

  },
// created() runs right away, this is where we make API requests
  created(){
    //This URL will usually have the link to a backend API which is to be used
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5') //Will return a promise (handle promises with .then and .catch to check for error)
      //response will have a value called data(todos array)
      .then(res => this.todos = res.data) //Filling todos array with todos we get back from the request from the URL

      .catch(err => console.log(err))


  }

}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
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
