<template>
  <div class="status-filter">
    <div class="label">Statut</div>

    <div class="segmented" role="tablist" aria-label="Filtrer par statut">
      <button
          v-for="filter in filters"
          :key="filter.value"
          type="button"
          class="segmented__btn"
          :class="{ active: currentFilter === filter.value }"
          @click="select(filter.value)"
      >
        {{ filter.label }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const filters = [
  { value: 'all', label: 'Tous' },
  { value: 'active', label: 'Actives' },
  { value: 'completed', label: 'Terminées' }
]

const currentFilter = ref('all')

const emit = defineEmits(['filter-change'])

function select(value) {
  currentFilter.value = value
  emit('filter-change', value)
}
</script>

<style scoped>
.status-filter {
  display: grid;
  gap: 8px;
}

.label {
  font-size: 12px;
  color: var(--muted);
}

.segmented {
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: 1fr;
  gap: 8px;
  padding: 6px;
  border-radius: 14px;
  border: 1px solid var(--border);
  background: rgba(0, 0, 0, 0.14);
}

.segmented__btn {
  height: 36px;
  border-radius: 12px;
  border: 1px solid transparent;
  background: transparent;
  color: var(--muted);
  cursor: pointer;
  transition: background 120ms ease, transform 120ms ease, color 120ms ease, border-color 120ms ease;
}

.segmented__btn:hover {
  background: rgba(255, 255, 255, 0.07);
  color: var(--text);
}

.segmented__btn.active {
  background: rgba(66, 184, 131, 0.18);
  border-color: rgba(66, 184, 131, 0.35);
  color: var(--text);
}

.segmented__btn:active {
  transform: translateY(1px);
}
</style>