<template>
  <div class="todoitem" v-bind:class="{'is-completed':todo.completed}">
      <input type="checkbox" v-on:change="markComplete"/>
      <p>{{todo.title}}</p>
      <button @click="$emit('del-todo',todo.id)" class="del">x</button>
  </div>
</template>

<script>
export default {
    name:"Todoitem",
    props:["todo"],
    methods:{
        markComplete(){
           // console.log("marked complete")
           this.todo.completed=!this.todo.completed
        }
    }
}
</script>

<style scoped>
    .todoitem {
        background-color: #f4f4f4;
        padding: 10px;
        border-bottom: burlywood 1px dotted;
    }

    .is-completed {
        text-decoration: line-through;
    }

    .del {
        background-color: red;
        color: white;
        cursor: pointer;
        float: right;
        padding: 5px 9px;
        border: none;
        border-radius: 50%;
    }


</style>