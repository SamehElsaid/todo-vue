<script setup>
import InputAdd from '@/components/InputAdd.vue'
import Todo from '@/components/TodoItem.vue'
import { ref, watch } from 'vue'

const toDos = ref(JSON.parse(localStorage.getItem('toDos')) ?? [])
const addTodo = (todo) => {
  console.log('run')
  toDos.value = [...toDos.value, todo]
}
const removeTodo = (index) => {
  console.log('run1')
  toDos.value = toDos.value.filter((_, i) => i !== index)
}

const clearCompletedTask = () => {
  console.log('run2')
  toDos.value = toDos.value.filter((todo) => !todo.completed)
}

const updateTodo = ({ index, completed }) => {
  console.log(index)
  console.log(completed)
  const newTodos = [...toDos.value]
  newTodos[index].completed = completed
  toDos.value = newTodos
}

const resetTodoList = () => {
  toDos.value = []
}

watch(
  () => toDos.value,
  (newVal) => {
    console.log(newVal)
    localStorage.setItem('toDos', JSON.stringify(newVal))
  },
  { deep: true }
)
</script>
<template>
  <main>
    <div class="w-full h-screen bg-gray-100 pt-8">
      <div class="bg-white p-3 max-w-md mx-auto">
        <InputAdd @add="addTodo" />
        <div class="mt-8">
          <ul>
            <Todo
              v-for="(todo, i) in toDos"
              :key="i"
              :todo="todo"
              :index="i"
              @remove="removeTodo"
              @update="updateTodo"
            />
          </ul>
        </div>
        <div class="mt-8">
          <button class="border-2 border-red-500 p-2 text-red-500" @click="clearCompletedTask">
            Clear Completed Task
          </button>
          <button
            class="border-2 border-indigo-500 p-2 text-indigo-500 ml-4"
            @click="resetTodoList"
          >
            Reset Todo List
          </button>
        </div>
      </div>
    </div>
  </main>
</template>
