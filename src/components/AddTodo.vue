<template>
  <div>
    <form @submit="addTodo">
      <input type="text" name="title" placeholder="Add Todo" v-model="title">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>

<script>
import uuid from 'uuid';
export default {
  name:'AddTodo',
  data:()=>{
    return{
      title:''
    }
  },
  methods:{
    addTodo(e){
      e.preventDefault();
      const newTodo={
        id: uuid.v4(),
        title:this.title,
        completed: false
      }
      console.log(newTodo);
      // Send up to parent
      this.$emit('add-todo',newTodo);
      this.title="";
    }
  }
}
</script>

<style scoped>
  form{
    display: flex;
  }
  input[type="text"]{
    flex:10;
    padding: 5px;
  }
  input[type="submit"]{
    flex:2;
  }
  .btn{
    padding: .5rem 2rem;
    outline: none;
    background:#333;
    color:#fff;
  }
</style>