<script setup>
import { useCounterStore } from '@/stores/counter'
import { reactive } from 'vue'
const counterStore = useCounterStore()

const emit = defineEmits(['add'])
const state = reactive({
  todo: ''
})
const updateTodo = () => {
  if (state.todo) {
    emit('add', { text: state.todo, completed: false })
    state.todo = ''
  } else {
    console.log('Please enter a task')
  }
}
</script>

<template>
  <div
    class="flex flex-col items-center justify-center p-5 rounded-md mb-5 border-dashed border-4 border-blue-400"
  >
    <h1 class="text-2xl font-bold text-center capitalize text-blue-400">pinia state management</h1>
    <p class="text-2xl font-bold">Count: {{ counterStore.count }}</p>
    <p class="text-2xl font-bold">Double Count: {{ counterStore.doubleCount }}</p>
    <button
      @click="counterStore.increment"
      class="mt-4 px-4 py-2 bg-blue-500 text-white rounded-lg"
    >
      Increment
    </button>
  </div>
  <form @submit.prevent="updateTodo" class="text-center">
    <h1 class="text-3xl font-bold">ToDo App</h1>
    <div class="mt-4 flex">
      <input
        class="w-80 border-b-2 border-gray-500 text-black"
        type="text"
        placeholder="Enter your task here"
        v-model="state.todo"
      />
      <button
        type="submit"
        class="ml-2 border-2 border-green-500 p-2 text-green-500 hover:text-white hover:bg-green-500 rounded-lg flex"
      >
        <svg
          class="h-6 w-6"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          stroke-width="2"
          stroke="currentColor"
          fill="none"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <path stroke="none" d="M0 0h24v24H0z" />
          <circle cx="12" cy="12" r="9" />
          <line x1="9" y1="12" x2="15" y2="12" />
          <line x1="12" y1="9" x2="12" y2="15" />
        </svg>
        <span>Add</span>
      </button>
    </div>
  </form>
</template>
