<template>
  <div class="app-container">
    <div class="counter-card">

      <header>
        <span class="label">Current Count</span>
        <h1 :class="{ 'positive': count > 0, 'negative': count < 0 }">{{ count }}</h1>
      </header>

      <div class="message-container">
        <transition name="fade">
          <span v-if="count < 0" class="badge warning">Vous êtes en dessous de 0</span>
          <span v-else-if="count > 100" class="badge success">Vous êtes au dessus de 100</span>
        </transition>
      </div>

      <div class="controls-grid">
        <button class="btn decrease" @click="decrement" @keyup.left="decrement">
          -1
        </button>

        <button class="btn reset" @click="reset" @keyup.delete="reset">
          Reset
        </button>

        <button class="btn increase" @click="increment" @keyup.right="increment">
          +1
        </button>
      </div>

      <div class="input-group">
        <label for="manual-input">Définir valeur</label>
        <input
            id="manual-input"
            type="number"
            placeholder="Entrer un nombre..."
            @input="e => incrementBy(e.target.valueAsNumber)"
        >
      </div>

    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue'

const count = ref(0);

function increment() {
  count.value++
}

function decrement() {
  count.value--
}

function reset() {
  count.value = 0
}

function incrementBy(amount) {
  if (!amount && amount !== 0) return;
  count.value = amount
}
</script>

<style scoped>
.app-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #f0f4f8;
  font-family: 'Inter', -apple-system, sans-serif;
}

.counter-card {
  background: white;
  padding: 3rem 2.5rem;
  border-radius: 24px;
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.01);
  text-align: center;
  width: 100%;
  max-width: 360px;
  transition: transform 0.2s;
}

.counter-card:hover {
  transform: translateY(-2px);
}

.label {
  text-transform: uppercase;
  font-size: 0.75rem;
  letter-spacing: 1.5px;
  color: #94a3b8;
  font-weight: 600;
}

h1 {
  font-size: 5rem;
  margin: 0.5rem 0 1rem 0;
  color: #1e293b;
  font-weight: 800;
  line-height: 1;
  font-variant-numeric: tabular-nums;
}

h1.positive {
  color: #42b883;
}

h1.negative {
  color: #ef4444;
}

.message-container {
  min-height: 30px;
  margin-bottom: 2rem;
  display: flex;
  justify-content: center;
}

.badge {
  font-size: 0.85rem;
  padding: 6px 12px;
  border-radius: 99px;
  font-weight: 500;
}

.badge.warning {
  background: #fee2e2;
  color: #991b1b;
}

.badge.success {
  background: #dcfce7;
  color: #166534;
}

.controls-grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 12px;
  margin-bottom: 2rem;
}

.btn {
  border: none;
  padding: 12px;
  border-radius: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 1rem;
}

.btn:active {
  transform: scale(0.95);
}

.decrease {
  background-color: #f1f5f9;
  color: #334155;
}

.decrease:hover {
  background-color: #e2e8f0;
}

.increase {
  background-color: #1e293b;
  color: white;
}

.increase:hover {
  background-color: #42b883;
}

.reset {
  background-color: transparent;
  border: 2px solid #f1f5f9;
  color: #64748b;
  font-size: 0.9rem;
}

.reset:hover {
  border-color: #fee2e2;
  color: #ef4444;
  background-color: #fff5f5;
}

.input-group {
  text-align: left;
  border-top: 1px solid #f1f5f9;
  padding-top: 1.5rem;
}

.input-group label {
  display: block;
  font-size: 0.8rem;
  color: #64748b;
  margin-bottom: 0.5rem;
}

input {
  width: 100%;
  padding: 12px;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 1rem;
  outline: none;
  color: #334155;
  transition: border-color 0.2s;
  box-sizing: border-box;
}

input:focus {
  border-color: #42b883;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>