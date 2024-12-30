<template>
  <div class="todo-list">
    <div class="add-todo">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo"
        placeholder="添加新的待办事项..."
      >
      <button @click="addTodo">添加</button>
    </div>

    <div class="todos">
      <TodoItem
        v-for="(todo, index) in visibleTodos"
        :key="todo.id"
        :todo="todo"
        @toggle="toggleTodo(index)"
        @delete="deleteTodo(index)"
        @dragstart="handleDragStart($event, index)"
        @dragend="handleDragEnd"
        @dragover.prevent
        @drop="handleDrop($event, index)"
      />
    </div>

    <div v-if="todos.length > 3" class="collapse-control">
      <button @click="isCollapsed = !isCollapsed">
        {{ isCollapsed ? '展开' : '折叠' }} ({{ hiddenCount }}项)
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'
import TodoItem from './TodoItem.vue'

// 从 LocalStorage 获取保存的待办事项，如果没有则使用空数组
const todos = ref(JSON.parse(localStorage.getItem('todos') || '[]'))
const newTodo = ref('')
const isCollapsed = ref(true)
const draggedItem = ref(null)

// 监听 todos 的变化，保存到 LocalStorage
watch(todos, (newTodos) => {
  localStorage.setItem('todos', JSON.stringify(newTodos))
}, { deep: true })  // 使用 deep 选项以监听数组内部的变化

const visibleTodos = computed(() => {
  return isCollapsed.value ? todos.value.slice(0, 3) : todos.value
})

const hiddenCount = computed(() => {
  return Math.max(0, todos.value.length - 3)
})

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      completed: false
    })
    newTodo.value = ''
  }
}

const toggleTodo = (index) => {
  todos.value[index].completed = !todos.value[index].completed
}

const deleteTodo = (index) => {
  todos.value.splice(index, 1)
}

const handleDragStart = (e, index) => {
  draggedItem.value = index
  e.dataTransfer.effectAllowed = 'move'
}

const handleDragEnd = () => {
  draggedItem.value = null
}

const handleDrop = (e, toIndex) => {
  const fromIndex = draggedItem.value
  if (fromIndex !== null) {
    const item = todos.value[fromIndex]
    todos.value.splice(fromIndex, 1)
    todos.value.splice(toIndex, 0, item)
  }
}

const checkAllCompleted = computed(() => {
  return todos.value.length > 0 && todos.value.every(todo => todo.completed)
})

watch(checkAllCompleted, (newValue) => {
  emit('update:allCompleted', newValue)
})

const emit = defineEmits(['update:allCompleted'])
</script>

<style scoped>
.todo-list {
  margin-top: 20px;
}

.add-todo {
  display: flex;
  margin-bottom: 20px;
}

.add-todo input {
  flex: 1;
  padding: 8px;
  margin-right: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: white;
  color: #333;
  outline: none;
}

.add-todo input:focus {
  border-color: #42b983;
}

.add-todo button {
  padding: 8px 16px;
  background: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.collapse-control {
  text-align: center;
  margin-top: 10px;
}

.collapse-control button {
  padding: 5px 10px;
  background: #f1f1f1;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  color: #333;
  font-size: 13px;
  font-weight: normal;
}
</style> 