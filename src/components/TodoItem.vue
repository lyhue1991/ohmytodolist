<template>
  <div 
    class="todo-item" 
    :class="{ completed: todo.completed }"
    draggable="true"
    @dragstart="$emit('dragstart', $event)"
    @dragend="$emit('dragend', $event)"
    @dragover.prevent
    @dragenter.prevent
  >
    <input 
      type="checkbox" 
      :checked="todo.completed"
      @change="$emit('toggle')"
    >
    <span class="todo-text">{{ todo.text }}</span>
    <button class="delete-btn" @click="$emit('delete')">×</button>
  </div>
</template>

<script setup>
defineProps({
  todo: {
    type: Object,
    required: true
  }
})

defineEmits(['toggle', 'delete', 'dragstart', 'dragend'])
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 4px 6px;
  margin: 2px 0;
  background: #fff;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  cursor: move;
  font-size: 14px;
}

.completed {
  opacity: 0.6;
}

.completed .todo-text {
  text-decoration: line-through;
  color: #999;
}

.todo-text {
  flex: none;
  margin: 0 10px;
  color: #333;
}

.delete-btn {
  margin-left: auto;
  border: none;
  background: none;
  color: #ff4757;
  font-size: 16px;
  cursor: pointer;
  padding: 0 4px;
}

.delete-btn:hover {
  color: #ff6b81;
}

input[type="checkbox"] {
  width: 14px;
  height: 14px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 3px;
  cursor: pointer;
  -webkit-appearance: none;
  appearance: none;
  position: relative;
}

input[type="checkbox"]:checked {
  background-color: #42b983;
  border-color: #42b983;
}

input[type="checkbox"]:checked::after {
  content: '✓';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 10px;
}
</style> 