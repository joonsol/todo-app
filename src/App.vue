<template>
  <div id="app">
   <todoHeader></todoHeader>
   <todoInput v-on:addTodo="addTodo"></todoInput>
   <todoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></todoList>
   <todoFooter v-on:removeAll="clearAll"></todoFooter>
  </div>
</template>

<script>
import todoHeader from './components/todoHeader.vue'
import todoInput from './components/todoInput.vue'
import todoList from './components/todoList.vue'
import todoFooter from './components/todoFooter.vue'

export default {
 data(){
   return{
     todoItems:[]
   }
 },
  methods:{
    addTodo(todoItem){
      localStorage.setItem(todoItem,todoItem);
      this.todoItems.push(todoItem)
    },
    clearAll(){
      localStorage.clear();
      this.todoItems=[];
    },
    removeTodo(todoItem,index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    }
  },
    created(){
    if(localStorage.length>0){
      for(let i=0;i<localStorage.length;i++){
        this.todoItems.push(localStorage.key(i))
      }
    }
  },
  components: {
   todoHeader:todoHeader,
   todoInput:todoInput,
   todoList:todoList,
   todoFooter:todoFooter,
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>