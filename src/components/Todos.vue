<template>
<div>
    <div v-for="todo in todoss" :key="todo.id">
        <!--h3>{{todo.title}}</h3-->
        <Todoitem v-bind:todo=todo v-on:del-todo="$emit('del-todo',todo.id)"></Todoitem>
    </div>
</div>

</template>

<script>
import Todoitem from "./Todoitem"

export default {
   name:"Todos",
   components:{
       Todoitem
   },
   props: ["todoss"]
}
</script>

<style scoped>

</style>