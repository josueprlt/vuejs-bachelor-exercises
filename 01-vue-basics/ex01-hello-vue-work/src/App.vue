<script setup>
import { ref } from 'vue'

const name = ref('Josué')
const currentDate = ref(new Date().toLocaleDateString('fr-FR', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' }).replace(',', ''))
</script>

<template>
  <div class="wrapper">
    <div class="card">
      <header>
        <h1>Hello Vue!</h1>
        <p class="greeting">Welcome, <span class="highlight">{{ name }}</span></p>
      </header>

      <main>
        <input v-model="name" type="text" placeholder="Enter your name...">
        <p class="date">{{ currentDate }}</p>
      </main>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f4f8;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
}

.card {
  background: white;
  padding: 3rem;
  border-radius: 16px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.05);
  text-align: center;
  width: 100%;
  max-width: 400px;
  transition: transform 0.2s;
}

.card:hover {
  transform: translateY(-2px);
}

h1 {
  color: #2c3e50;
  font-size: 2rem;
  margin-bottom: 0.5rem;
  font-weight: 700;
}

.greeting {
  color: #64748b;
  font-size: 1.1rem;
  margin-bottom: 2rem;
}

.highlight {
  color: #42b883;
  font-weight: 600;
}

input {
  width: 100%;
  padding: 12px 16px;
  font-size: 1rem;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  outline: none;
  transition: all 0.3s ease;
  color: #334155;
  box-sizing: border-box;
}

input:focus {
  border-color: #42b883;
  box-shadow: 0 0 0 3px rgba(66, 184, 131, 0.1);
}

input::placeholder {
  color: #94a3b8;
}

.date {
  margin-top: 1.5rem;
  color: #94a3b8;
  font-size: 0.85rem;
  text-transform: capitalize;
  letter-spacing: 0.5px;
}
</style>