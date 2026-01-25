<template>
  <div class="container">
    <h1>Hello Vue!</h1>
    <p class="greeting">Welcome, {{ name }}! 🎉</p>
    
    <div class="input-group">
      <label for="name-input">Enter your name:</label>
      <input 
        id="name-input"
        v-model="name" 
        type="text" 
        placeholder="Your name here..."
      />
    </div>
    
    <p class="date">{{ currentDate }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Reactive data
const name = ref('Student')
const currentDate = ref(new Date().toLocaleDateString('en-US', {
  weekday: 'long',
  year: 'numeric',
  month: 'long',
  day: 'numeric'
}))
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 50px auto;
  padding: 30px;
  text-align: center;
  font-family: Arial, sans-serif;
}

h1 {
  color: #42b883;
  font-size: 3rem;
  margin-bottom: 20px;
}

.greeting {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 30px;
}

.input-group {
  margin-bottom: 30px;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
  color: #555;
}

input {
  padding: 12px 20px;
  font-size: 1rem;
  border: 2px solid #42b883;
  border-radius: 8px;
  width: 100%;
  max-width: 300px;
  transition: all 0.3s ease;
}

input:focus {
  outline: none;
  border-color: #35495e;
  box-shadow: 0 0 10px rgba(66, 184, 131, 0.3);
}

.date {
  color: #666;
  font-size: 1rem;
  margin-top: 30px;
}
</style>
