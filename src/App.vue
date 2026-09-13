<script setup>
import { ref, computed, watch } from 'vue'
import Navbar from './components/Navbar.vue'
import TaskInput from './components/TaskInput.vue'
import TaskList from './components/TaskList.vue'


const userName = ref('')
const searchQuery = ref('')
const currentFilter = ref('all')


const savedTasks = JSON.parse(localStorage.getItem('pro_tasks'))
const tasks = ref(savedTasks || [])

watch(tasks, (newTasks) => {
  localStorage.setItem('pro_tasks', JSON.stringify(newTasks))
}, { deep: true })

 
const totalTasks = computed(() => tasks.value.length)
const completedTasks = computed(() => tasks.value.filter(task => task.completed).length)

// 整合「狀態篩選」與「關鍵字搜尋」的計算屬性
const filteredTasks = computed(() => {
  let result = tasks.value
  
  // 狀態篩選 (全部 / 未完成 / 已完成)
  if (currentFilter.value === 'active') {
    result = result.filter(t => !t.completed)
  } else if (currentFilter.value === 'completed') {
    result = result.filter(t => t.completed)
  }
  
  if (searchQuery.value.trim() !== '') {
    const keyword = searchQuery.value.trim().toLowerCase()
    result = result.filter(t => t.text.toLowerCase().includes(keyword))
  }
  
  return result
})

const handleAddTask = (taskText) => {
  tasks.value.push({
    id: Date.now(),
    text: taskText,
    completed: false
  })
}

const handleToggleTask = (id) => {
  const task = tasks.value.find(t => t.id === id)
  if (task) task.completed = !task.completed
}

const handleDeleteTask = (id) => {
  tasks.value = tasks.value.filter(t => t.id !== id)
}

const handleClearCompleted = () => {
  tasks.value = tasks.value.filter(t => !t.completed)
}

const login = () => {
  userName.value = '工程師John'
}

const logout = () => {
  userName.value = ''
}
</script>

<template>
  <Navbar :userName="userName" @login="login" @logout="logout"/>

  <main class="main-content">
    <div class="task-stats">
      總任務：{{ totalTasks }} 個 | 已完成：{{ completedTasks }} 個
    </div>
    <!-- 新增任務輸入框 -->
    <TaskInput @add-task="handleAddTask"/>

    <!-- 搜尋任務輸入框 -->
    <div class="search-box">
      <input 
        type="text"
        v-model="searchQuery"
        placeholder="搜尋任務..."
      />
    </div>

    <!-- 篩選按鈕列與清除按鈕 -->
    <div class="filter-container">
      <div class="filter-buttons">
        <button 
          :class="{ active: currentFilter === 'all' }"
          @click="currentFilter = 'all'"
        >全部</button>
        <button 
          :class="{ active: currentFilter === 'active' }"
          @click="currentFilter = 'active'"
        >未完成</button>
        <button 
          :class="{ active: currentFilter === 'completed' }"
          @click="currentFilter = 'completed'"
        >已完成</button>
      </div>

      <button class="clear-btn" @click="handleClearCompleted">清除已完成</button>
    </div>

    <TaskList
      :tasks="filteredTasks"
      @toggle-task="handleToggleTask"
      @delete-task="handleDeleteTask"
    />
  </main>
</template>

<style>
body {
  margin: 0;
  background-color: #f8fafc;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}
</style>

<style scoped>
.main-content {
  max-width: 600px;
  margin: 40px auto;
  padding: 32px;
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
}

.task-stats {
  margin-bottom: 12px;
  font-size: 14px;
  color: #64748b;
}

.search-box {
  margin-top: 16px;
  margin-bottom: 4px;
}

.search-box input {
  width: 100%;
  padding: 10px 14px;
  box-sizing: border-box;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-size: 14px;
  outline: none;
  transition: border-color 0.2s ease;
}

.search-box input:focus {
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.filter-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
  margin-top: 16px;
}

.filter-buttons {
  display: flex;
  gap: 8px;
}

.filter-buttons button {
  padding: 6px 12px;
  border: 1px solid #cbd5e1;
  background-color: #ffffff;
  color: #64748b;
  border-radius: 6px;
  cursor: pointer;
  font-size: 13px;
  transition: all 0.2s ease;
}

.filter-buttons button:hover {
  background-color: #f1f5f9;
}

.filter-buttons button.active {
  background-color: #3b82f6;
  color: #ffffff;
  border-color: #3b82f6;
}

.clear-btn {
  padding: 6px 12px;
  border: 1px solid #fecaca;
  background-color: #fef2f2;
  color: #dc2626;
  border-radius: 6px;
  cursor: pointer;
  font-size: 13px;
  transition: all 0.2s ease;
}

.clear-btn:hover {
  background-color: #fee2e2;
}
</style>