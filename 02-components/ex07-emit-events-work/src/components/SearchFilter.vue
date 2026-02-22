<template>
  <div class="search-filter">
    <label class="label" for="task-search">Recherche</label>

    <div class="control">
      <input
          id="task-search"
          :value="modelValue"
          @input="$emit('update:modelValue', $event.target.value)"
          type="text"
          placeholder="Rechercher une tâche…"
          class="input"
      >

      <button
          v-if="modelValue"
          class="btn btn--ghost"
          type="button"
          @click="$emit('update:modelValue', '')"
          aria-label="Effacer la recherche"
          title="Effacer"
      >
        Clear
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  modelValue: {
    type: String,
    default: ''
  }
})

defineEmits(['update:modelValue'])
</script>

<style scoped>
.search-filter {
  display: grid;
  gap: 8px;
}

.label {
  font-size: 12px;
  color: var(--muted);
}

.control {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 10px;
  align-items: center;
}

.input {
  width: 100%;
  height: 42px;
  padding: 0 12px;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(0, 0, 0, 0.18);
  color: var(--text);
  outline: none;
  transition: border-color 120ms ease, box-shadow 120ms ease, transform 120ms ease;
}

.input::placeholder {
  color: rgba(255, 255, 255, 0.45);
}

.input:focus {
  border-color: rgba(66, 184, 131, 0.55);
  box-shadow: var(--ring);
}

.btn {
  height: 42px;
  padding: 0 12px;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.08);
  color: var(--text);
  cursor: pointer;
  transition: transform 120ms ease, background 120ms ease, border-color 120ms ease;
}

.btn:hover {
  transform: translateY(-1px);
  background: rgba(255, 255, 255, 0.10);
}

.btn:active {
  transform: translateY(0);
}

.btn--ghost {
  background: transparent;
}
</style>