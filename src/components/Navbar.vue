<script setup>
defineProps(['userName'])
defineEmits(['login', 'logout'])
</script>

<template>
  <nav class="navbar">
    <div class="logo">ProTask</div>
    <div class="user-menu">
      <span v-if="userName">歡迎，{{ userName }}</span>
      <button v-if="userName" @click="$emit('logout')">登出</button>
      <button v-else @click="$emit('login')">登入</button>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 32px;
  background-color: #ffffff;
  border-bottom: 1px solid #e2e8f0;
}
.logo {
  font-weight: 700;
  font-size: 18px;
  color: #0f172a;
}
.user-menu {
  display: flex;
  align-items: center;
  gap: 16px;
}
</style>