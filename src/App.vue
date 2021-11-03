<template>
  <div class="container">

    <h2>To-Do List</h2>
    <TodoSimpleForm @add-todo="addTodo"/>
        
    <div v-if="!todos.length">추가된 Todo가 없습니다.</div>

    <TodoList :todos="todos" @toggle-todo="toggleTodo" @delete-todo="deleteTodo"/>

    <button @click="ViewTodos()" >View Todos</button>
  </div>
</template>

<script>
import {ref} from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';

export default {
  components:{
    TodoSimpleForm,
    TodoList 
  },
  setup(){
    
    const todos = ref([]);
    
    const todoStyle = {
      textDecoration : 'line-through',
      color : 'gray'
    }

    const addTodo = (todo) => {
      todos.value.push(todo);
    }

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    const toggleTodo = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
    }

    const ViewTodos = () => {
      console.log(todos.value);
    }

    return {
      todoStyle,
      todos,
      addTodo,
      deleteTodo,
      toggleTodo,
      ViewTodos
    };

  }
}
</script>

<style>
  .todo{
    color: gray;
    text-decoration:  line-through;
  }

</style>
