<template>
<div class="todo__item" v-bind:class="{'is__complete':todo.completed}">
  <h3> <input type="checkbox" name="" id="" v-on:change="markComplete"> &nbsp; {{todo.title}}</h3>
  <button @click="$emit('delete-todo',todo.id)">X</button>
</div>
</template>
<script>
export default {
  name:'TodoItem',
  props:['todo'],
  methods:{
    markComplete(){
      this.todo.completed=!this.todo.completed;
    }
  }
}
</script>
<style scoped>
 .is__complete{
   text-decoration: line-through;
 }
</style>