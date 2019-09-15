<template>
  <div>
    <AddTodo />
    <Todos v-bind:todos="todos" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
export default {
  name:'Home',
  components:{
    Todos,
    AddTodo
  },
  props:['todos']
}
</script>