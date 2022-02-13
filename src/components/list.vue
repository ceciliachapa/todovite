<script setup>
import useTodos from "../composables/useTodos";
const { pending, completed, changeStatus } = useTodos();
defineProps({
  isCompleted: {
    default: false,
    type: Boolean,
  },
});
</script>

<template>
  <div class="w-1/4">
    <h3
      class="font-bold text-2xl text-center"
      :class="isCompleted ? 'text-yellow-800' : 'text-green-900'"
    >
      {{ isCompleted ? "Completed ✔" : "Pending ⏸" }}
    </h3>
    <ul class="pt-8 space-y-2">
      <li
        v-for="todo in isCompleted ? completed : pending"
        :key="todo.id"
        @click="changeStatus(todo.id)"
        :class="
          isCompleted
            ? 'text-green-700 hover:bg-red-900'
            : 'text-yellow-600 hover:bg-green-800'
        "
        class="
          w-full
          px-4
          py-2
          font-bold
          text-center
          transition-colors
          duration-500
          bg-gray-300
          rounded-lg
          hover:border-dotted
          hover:border-4
          hover:cursor-pointer
          hover:text-gray-200
        "
      >
        {{ todo.content }}
      </li>
    </ul>
  </div>
</template>