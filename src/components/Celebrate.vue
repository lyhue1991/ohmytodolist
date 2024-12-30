<template>
  <div class="celebrate">
    <div class="rose">🌹</div>
    <div class="message">恭喜你完成了所有待办事项！</div>
  </div>
</template>

<script setup>
</script>

<style scoped>
.celebrate {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}

.rose {
  font-size: 100px;
  animation: bounce 1s infinite;
}

.message {
  margin-top: 20px;
  font-size: 24px;
  color: #42b983;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}
</style> 