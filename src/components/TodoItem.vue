<script setup>
const emit = defineEmits(['remove'])
const { todo, index } = defineProps({
  todo: {
    type: {
      text: String,
      completed: Boolean
    },
    required: true
  },
  index: {
    type: Number,
    required: true
  }
})
console.log('s')
const removeTodo = () => {
  emit('remove', index)
}
const updateTodo = () => {
  emit('update', { index, completed: !todo.completed })
}
</script>

<template>
  <li class="p-2 rounded-lg">
    <div class="flex align-middle flex-row justify-between">
      <div class="p-2">
        <input
          type="checkbox"
          :checked="todo.completed"
          @change="updateTodo"
          class="h-6 w-6"
          value="true"
        />
      </div>
      <div class="p-2">
        <p class="text-lg text-black" :class="todo.completed ? 'line-through' : ''">
          {{ todo.text }}
        </p>
      </div>
      <button @click="removeTodo" class="flex text-red-500 border-2 border-red-500 p-2 rounded-lg">
        <svg
          class="h-6 w-6 text-red-500"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <circle cx="12" cy="12" r="10" />
          <line x1="15" y1="9" x2="9" y2="15" />
          <line x1="9" y1="9" x2="15" y2="15" />
        </svg>
        <span>Remove</span>
      </button>
    </div>
    <hr class="mt-2" />
  </li>
</template>
