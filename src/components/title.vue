<script setup>
import { ref } from 'vue';
import useTodos from '../composables/useTodos';
const { addTodo } = useTodos();
const newTodo = ref('');
const add = () => {
  if (newTodo.value) {
    addTodo(newTodo.value);
    newTodo.value = '';
  }
};
</script>

<template>
  <h1
    class="pb-4 font-mono text-6xl font-bold tracking-tight text-center text-purple-900 "
  >
    📑 My To Do App
  </h1>
  <input
    @change="add"
    v-model="newTodo"
    type="text"
    class="justify-center w-1/3 px-4 py-2 mx-auto text-xl text-center align-middle rounded-lg "
    placeholder="New To Do item"
  />
</template>