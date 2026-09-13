<script setup>
defineProps(['tasks'])
defineEmits(['toggle-task', 'delete-task'])

</script>

<template>
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
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

ul li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  margin-bottom: 8px;
  background-color: #f8fafc;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  transition: background-color 0.2s ease;
}

ul li:hover {
  background-color: #f1f5f9;
}

.task-text {
  cursor: pointer;
  font-size: 14px;
  color: #1e293b;
  word-break: break-all;
  flex: 1;
  margin-right: 12px;
}

.completed {
  text-decoration: line-through;
  color: #94a3b8;
}

ul li button {
  background-color: #ef4444;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 6px 12px;
  font-size: 12px;
  cursor: pointer;
}

ul li button:hover {
  background-color: #dc2626;
}
</style>