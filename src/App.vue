<script setup>
import { ref, computed } from "vue";
const newTodo = ref("");
const todos = ref([]);
const pending = computed(() => {
  return todos.value.filter((todo) => !todo.done);
});
const completed = computed(() => {
  return todos.value.filter((todo) => todo.done);
});
const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: todos.value.length,
      content: newTodo.value,
      done: false,
    });
    newTodo.value = "";
  }
};
const changeStatus = (id) => {
  const todo = todos.value.find((todo) => todo.id === id);
  todo.done = !todo.done;
};
</script>

<template>
  <div class="min-h-screen bg-gray-300">
    <div class="container flex flex-col pt-8 mx-auto space-y-8">
      <h1
        class="
          pb-4
          text-6xl
          font-mono
          tracking-tight
          text-center
          font-bold
          text-purple-900
        "
      >
        📑 My To Do App
      </h1>
      <div class="flex justify-around">
        <input
          @change="addTodo"
          v-model="newTodo"
          type="text"
          class="align-middle px-4 py-2 text-xl text-center rounded-lg w-1/2"
          placeholder="New To Do item"
        />
      </div>
      <div class="flex justify-around">
        <div class="w-1/3">
          <h3 class="text-2xl text-center font-bold text-yellow-800">
            Pending ⏸
          </h3>
          <ul class="pt-8 space-y-4">
            <li
              v-for="todo in pending"
              :key="todo.id"
              @click="changeStatus(todo.id)"
              class="
                w-full
                px-4
                py-2
                font-bold
                text-center text-yellow-600
                transition-colors
                duration-500
                bg-gray-300
                rounded-lg
                hover:cursor-pointer
                hover:border-dotted
                hover:border-4
                hover:bg-yellow-800
                hover:text-gray-200
              "
            >
              {{ todo.content }}
            </li>
          </ul>
        </div>
        <div class="w-1/3">
          <h3 class="font-bold text-2xl text-center text-green-900">
            Completed ✔
          </h3>
          <ul class="pt-8 space-y-4">
            <li
              v-for="todo in completed"
              :key="todo.id"
              @click="changeStatus(todo.id)"
              class="
                w-full
                px-4
                py-2
                font-bold
                text-center text-green-700
                transition-colors
                duration-500
                bg-gray-300
                rounded-lg
                hover:border-dotted
                hover:border-4
                hover:cursor-pointer
                hover:bg-red-900
                hover:text-gray-200
              "
            >
              {{ todo.content }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
