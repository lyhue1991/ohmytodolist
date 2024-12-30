<template>
  <div class="app-container">
    <h1>{{ currentDate }}</h1>
    <TodoList v-model:allCompleted="allCompleted" />
    <Celebrate v-if="allCompleted" />
  </div>
</template>

<script setup>
import TodoList from './components/TodoList.vue'
import Celebrate from './components/Celebrate.vue'
import { ref, onMounted } from 'vue'

const allCompleted = ref(false)
const currentDate = ref('')

onMounted(() => {
  // 格式化当前日期为 yyyy-mm-dd
  const now = new Date()
  const year = now.getFullYear()
  const month = String(now.getMonth() + 1).padStart(2, '0')
  const day = String(now.getDate()).padStart(2, '0')
  currentDate.value = `${year}-${month}-${day}`
})
</script>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  color: #666;
  font-size: 1.2em;
}

.date {
  font-size: 1.2em;
  color: #666;
  font-weight: bold;
}
</style>
