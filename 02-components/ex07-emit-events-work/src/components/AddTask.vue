<template>
  <form @submit.prevent="handleSubmit" class="add-task-form">
    <div class="header">
      <h2 class="title">Ajouter une tâche</h2>
      <p class="subtitle">Un petit pas pour toi, un grand pas pour ta todo.</p>
    </div>

    <div class="field">
      <label class="label" for="task-title">Titre</label>
      <input
          id="task-title"
          v-model="title"
          type="text"
          placeholder="Ex: Réviser Vue 3"
          class="input"
      >
    </div>

    <div class="field">
      <label class="label" for="task-desc">Description (optionnel)</label>
      <textarea
          id="task-desc"
          v-model="description"
          placeholder="Quelques détails utiles…"
          class="textarea"
          rows="3"
      ></textarea>
    </div>

    <div class="actions">
      <button class="btn btn--primary" type="submit" :disabled="!title.trim()">
        Add Task
      </button>

      <button
          class="btn btn--ghost"
          type="button"
          :disabled="!title && !description"
          @click="clearForm"
      >
        Reset
      </button>
    </div>

    <p v-if="error" class="error" role="alert">{{ error }}</p>
  </form>
</template>

<script setup>
import { ref } from 'vue'

const title = ref('')
const description = ref('')
const error = ref('')

const emit = defineEmits(['add-task'])

function clearForm() {
  title.value = ''
  description.value = ''
  error.value = ''
}

function handleSubmit() {
  if (!title.value.trim()) {
    error.value = 'Le titre est obligatoire'
    return
  }

  const newTask = {
    id: Date.now(),
    title: title.value,
    description: description.value,
    completed: false,
    createdAt: new Date().toISOString()
  }

  emit('add-task', newTask)
  clearForm()
}
</script>

<style scoped>
.add-task-form {
  display: grid;
  gap: 12px;
}

.header {
  display: grid;
  gap: 4px;
  margin-bottom: 2px;
}

.title {
  margin: 0;
  font-size: 16px;
  letter-spacing: -0.01em;
}

.subtitle {
  margin: 0;
  font-size: 13px;
  color: var(--muted);
}

.field {
  display: grid;
  gap: 8px;
}

.label {
  font-size: 12px;
  color: var(--muted);
}

.input,
.textarea {
  width: 100%;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(0, 0, 0, 0.18);
  color: var(--text);
  outline: none;
  padding: 10px 12px;
  transition: border-color 120ms ease, box-shadow 120ms ease;
}

.input {
  height: 42px;
}

.textarea {
  resize: vertical;
  min-height: 84px;
}

.input::placeholder,
.textarea::placeholder {
  color: rgba(255, 255, 255, 0.45);
}

.input:focus,
.textarea:focus {
  border-color: rgba(66, 184, 131, 0.55);
  box-shadow: var(--ring);
}

.actions {
  display: flex;
  gap: 10px;
  align-items: center;
}

.btn {
  height: 40px;
  padding: 0 14px;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.08);
  color: var(--text);
  cursor: pointer;
  transition: transform 120ms ease, background 120ms ease, border-color 120ms ease, opacity 120ms ease;
}

.btn:hover {
  transform: translateY(-1px);
  background: rgba(255, 255, 255, 0.10);
}

.btn:active {
  transform: translateY(0);
}

.btn:disabled {
  opacity: 0.55;
  cursor: not-allowed;
  transform: none;
}

.btn--primary {
  border-color: rgba(66, 184, 131, 0.35);
  background: linear-gradient(180deg, rgba(66, 184, 131, 0.25), rgba(66, 184, 131, 0.14));
}

.btn--ghost {
  background: transparent;
}

.error {
  margin: 0;
  color: rgba(255, 90, 106, 0.95);
  font-size: 13px;
}
</style>