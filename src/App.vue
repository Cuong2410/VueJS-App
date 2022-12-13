<template>
  
  <h1 class="text-center text-2xl leading-tight font-bold my-5">ToDo App</h1>
  <form class="flex flex-col w-full" @submit.prevent="addTodo()">
    <label class="text-sm font-bold">New ToDo</label>
    <input class="text-lg px-12 bg-inherit box-border border-solid border-2 border-white border-opacity-50 mb-12 mt-6" v-model="newTodo" name="newTodo" autocomplete="off">
    <button class="text-black mt-6 mb-12 font-bold text-lg border-solid border-1 bg-indigo-300 text-base h-12">Add ToDo</button>
  </form>
  <h2 class="text-xl text-white border-solid border-white border-b-2 border-opacity-50">ToDo List</h2>
  <ul class="p-10">
    <li class="table" v-for="(todo, index) in todos" :key="index">
      <span class="color-text" :class="{ 'done-task': todo.done }" @click="doneTodo(todo)">
        {{ todo.name }} - {{ index }} {{ todo.done }}</span>
      <button class="button-remove" @click="removeTodo(index)">Remove</button>
    </li>
  </ul>
  <h4 v-if="todos.length === 0">Empty list.</h4>
</template>

<script setup>
import { ref } from 'vue';

const todos = ref([])
const newTodo = ref('')


function addTodo() {
  if (newTodo.value) {
    todos.value.push({
      done: false,
      name: newTodo.value
    });
    newTodo.value = '';
  }
}
function removeTodo(index) {
  todos.value.splice(index, 1);
}
function doneTodo(todo) {
  todo.done = !todo.done
}
</script>

<style scoped>
.done-task {
  text-decoration: line-through;
  color: red !important;
}

.table {
  list-style-type: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 2px solid #ffc107;
  padding: 12px 24px;
  border-radius: 6px;
  margin-bottom: 12px;
}

.button-remove {
  cursor: pointer;
  background-color: #a0a4d9;
  border: 1px solid #a0a4d9;
  color: #1f2023;
  font-weight: 700;
  outline: none;
  border-radius: 6px;
}

/* .color-text{
  color: aqua;
} */
</style>
