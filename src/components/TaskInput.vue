<script setup>
import { ref } from 'vue'
defineProps({
    tasks: Array
})
const text = ref('')
const emit = defineEmits(['add-task'])

const submitTask = () => {
  if (!text.value.trim()) return
  emit('add-task', text.value)
  text.value = ''
}
</script>

<template>
  <div class="task-input-container">
    <input 
      v-model="text" 
      type="text" 
      placeholder="請輸入任務..." 
      @keyup.enter="submitTask"
    />
    <button @click="submitTask" class="btn-primary">新增任務</button>
  </div>
  <ul>
      <li v-for="task in tasks" :key="task.id">
          <span
          @click="$emit('toggle-task', task.id)"
          :class="{ completed: task.completed}"
          class="task-text"
          >
          {{  task.text }}   
        </span>
        <button @click="$emit('delete-task', task.id)">刪除</button>
    </li>
</ul>
</template>

<style scoped>
.task-input-container {
  display: flex;
  gap: 12px;
  margin-bottom: 24px;
}
input {
  flex: 1;
  padding: 10px 16px;
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  font-size: 14px;
}
</style>