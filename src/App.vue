<template>
  <div class="wrapper-todo">

    <div class="title has-text-centered has-text-white">
      My Todo List:
    </div>
    <form @submit.prevent="addToDo">
      <div class="field is-grouped mb-5">
  <p class="control is-expanded">
    <input class="input" type="text" placeholder="Add todo" v-model="newTodoContent">
  </p>
  <p class="control">
    <button :disabled="!newTodoContent" class="button is-info">
      Add
    </button>
  </p>
  </div>
    </form>
    
  <div class="card mb-5" :key="todo.id" v-for="todo in todos" :class="{'has-background-success-light': todo.done}">
  <div class="card-content">
    <div class="content">
      <div class="columns is-mobile is-vcentered">
        <div class="column" :class="{'has-text-success line-through': todo.done}">{{ todo.content }}</div>
        <div class="column">done: {{ todo.done }}</div>
        <div class="column is-5 has-text-right">
      <button class="button is-lite" :class="todo.done ? 'is-success' : 'is-light'" @click="toggleDone(todo.id)">&check;</button>
    <button class="button is-danger ml-2" @click="deleteToDo(todo.id)">&cross;</button>
    </div>
  </div>
  </div>
  </div>
</div>
</div>
</template>

<script setup>
// import
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'

// todo
const todos = ref([
  {  
  id: '1',
  content: 'hello gays',
  done: false
  },
  {  
  id: '2',
  content: 'check this',
  done: true
  },
]);

// add todo 
const newTodoContent = ref("") 

const addToDo = () => {
  const newToDo = {
    id: uuidv4(),
  content: newTodoContent.value,
  done: false
  };
  todos.value.unshift(newToDo);
  newTodoContent.value = "";
}

// delete todo
const deleteToDo = (id) => {
  todos.value = todos.value.filter(todo => todo.id != id);
}

// done todo 
const toggleDone = (id) => {
  const index = todos.value.findIndex(todo => todo.id === id);
  todos.value[index].done = !todos.value[index].done
}
</script>

<style>
@import 'bulma/css/bulma.min.css';

.wrapper-todo{
  max-width: 600px;
  padding: 20px;
  margin: 0 auto;
}
.input{
  width: 300px;
}
.line-through{
  text-decoration: line-through;
}
</style>