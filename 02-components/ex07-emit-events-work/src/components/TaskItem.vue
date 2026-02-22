<template>
  <article class="task-item" :class="{ completed: task.completed }">
    <div class="task-main">
      <div class="task-top">
        <h3 class="task-title">{{ task.title }}</h3>
        <span class="badge" :class="task.completed ? 'badge--done' : 'badge--todo'">
          {{ task.completed ? 'Terminée' : 'Active' }}
        </span>
      </div>

      <p v-if="task.description" class="task-description">{{ task.description }}</p>

      <div class="task-meta">
        <span class="task-date">Créée : {{ task.createdAt }}</span>
      </div>
    </div>

    <div class="task-actions">
      <button
          type="button"
          class="btn"
          :class="task.completed ? 'btn--muted' : 'btn--primary'"
          @click="$emit('toggle-complete', task.id)"
      >
        {{ task.completed ? 'Undo' : 'Complete' }}
      </button>

      <button type="button" class="btn btn--ghost" @click="$emit('edit', task.id)">
        Edit
      </button>

      <button type="button" class="btn btn--danger" @click="handleDelete">
        Delete
      </button>
    </div>
  </article>
</template>

<script setup>
const props = defineProps({
  task: {
    type: Object,
    required: true
  }
})

const emit = defineEmits({
  'toggle-complete': (id) => {
    return typeof id === 'number'
  },
  'edit': (id) => {
    return typeof id === 'number'
  },
  'delete': (id) => {
    return typeof id === 'number'
  }
})

function handleDelete() {
  if (confirm('Are you sure you want to delete this task?')) {
    emit('delete', props.task.id)
  }
}
</script>

<style scoped>
.task-item {
  display: grid;
  grid-template-columns: 1fr;
  gap: 12px;
  padding: 14px;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.07), rgba(0, 0, 0, 0.14));
  box-shadow: 0 10px 26px rgba(0, 0, 0, 0.22);
}

@media (min-width: 720px) {
  .task-item {
    grid-template-columns: 1fr auto;
    align-items: center;
  }
}

.task-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
}

.task-title {
  margin: 0;
  font-size: 15px;
  letter-spacing: -0.01em;
}

.task-description {
  margin: 8px 0 0;
  color: var(--muted);
  font-size: 13px;
  line-height: 1.35;
}

.task-meta {
  margin-top: 10px;
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.task-date {
  font-size: 12px;
  color: rgba(255, 255, 255, 0.55);
}

.badge {
  font-size: 12px;
  padding: 6px 10px;
  border-radius: 999px;
  border: 1px solid var(--border);
  color: var(--text);
  background: rgba(255, 255, 255, 0.07);
}

.badge--todo {
  border-color: rgba(255, 204, 102, 0.40);
  background: rgba(255, 204, 102, 0.14);
}

.badge--done {
  border-color: rgba(66, 184, 131, 0.38);
  background: rgba(66, 184, 131, 0.16);
}

.task-actions {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  justify-content: flex-start;
}

.btn {
  height: 36px;
  padding: 0 12px;
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

.btn--primary {
  border-color: rgba(66, 184, 131, 0.35);
  background: linear-gradient(180deg, rgba(66, 184, 131, 0.25), rgba(66, 184, 131, 0.14));
}

.btn--muted {
  background: rgba(255, 255, 255, 0.06);
  color: rgba(255, 255, 255, 0.78);
}

.btn--ghost {
  background: transparent;
}

.btn--danger {
  border-color: rgba(255, 90, 106, 0.35);
  background: linear-gradient(180deg, rgba(255, 90, 106, 0.22), rgba(255, 90, 106, 0.12));
}

.completed {
  opacity: 0.82;
}

.completed .task-title {
  text-decoration: line-through;
  color: rgba(255, 255, 255, 0.78);
}
</style>