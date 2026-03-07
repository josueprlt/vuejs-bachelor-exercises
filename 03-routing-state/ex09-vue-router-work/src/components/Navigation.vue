<template>
  <nav class="navigation">
    <div class="logo">MyBlog</div>
    <ul class="nav-links">
      <li>
        <RouterLink to="/">Home</RouterLink>
      </li>
      <li>
        <RouterLink to="/blog">Blog</RouterLink>
      </li>
      <li>
        <RouterLink to="/about">About</RouterLink>
      </li>
      <li>
        <RouterLink :to="{ name: 'profile', params: { username: 'johndoe' } }">
          Profile
        </RouterLink>
      </li>
      <li>
        <RouterLink to="/dashboard">Dashboard</RouterLink>
      </li>
    </ul>
    <button @click="toggleAuth" class="auth-btn">
      {{ isAuthenticated ? 'Logout' : 'Login' }}
    </button>
  </nav>
</template>

<script setup>
import {ref, onMounted} from 'vue'

const isAuthenticated = ref(false)

onMounted(() => {
  isAuthenticated.value = localStorage.getItem('isAuthenticated') === 'true'
})

function toggleAuth() {
  isAuthenticated.value = !isAuthenticated.value
  localStorage.setItem('isAuthenticated', isAuthenticated.value)
}
</script>

<style scoped>
.navigation {
  display: flex;
  align-items: center;
  gap: 20px;
  padding: 15px 30px;
  background: #2c3e50;
  color: white;
}

.logo {
  font-size: 24px;
  font-weight: bold;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 20px;
  margin: 0;
  padding: 0;
  flex: 1;
}

.nav-links a {
  color: white;
  text-decoration: none;
  padding: 8px 16px;
  border-radius: 4px;
  transition: background 0.3s;
}

.nav-links a:hover {
  background: rgba(255, 255, 255, 0.1);
}

.nav-links a.router-link-active {
  background: #42b883;
}

.auth-btn {
  padding: 8px 16px;
  background: #42b883;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>