<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todoss="todos" v-on:del-todo="deleteTodo"></Todos>
  </div>
</template>

<script>
import Todos from "../components/Todos"
import AddTodo from "../components/AddTodo"
import axios from 'axios'

export default {
  name: 'Home',
  components: {
   Todos,
   AddTodo
  },

  data(){
    return {
      todos:[]
    }
  },
  methods: {
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res=>{
        console.log(res)
        this.todos=this.todos.filter(todo => todo.id != id )
      })
      .catch(err => console.log(err))
    },

    addTodo(newTodo){
      const {title,completed}=newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos',{title,completed})
      .then(res => {
        this.todos=[...this.todos,res.data];
        console.log(res)
      })
      .catch(err => console.log(err))
    }
  },
  created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos=res.data)
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
 line-height:  1.4;
}

.btn {
  display: inline-block;
  background: #555;
  color:#fff;
  cursor: pointer;
  padding: 7px 20px;
  border: none;
}

.btn:hover {
  background: #666;
}
</style>
