<template>
  <div class="app">
    <header class="app-header">
      <div class="app-header__inner">
        <h1 class="app-title">Task Manager</h1>
        <p class="app-subtitle">Simple, clean, modern.</p>
      </div>
    </header>

    <main class="app-main">
      <section class="card">
        <AddTask @add-task="addTask" />
      </section>

      <section class="card card--filters">
        <div class="filters">
          <SearchFilter v-model="searchQuery" />
          <StatusFilter @filter-change="handleFilterChange" />
        </div>

        <div class="task-stats">
          <div class="stat">
            <div class="stat__label">Total</div>
            <div class="stat__value">{{ tasks.length }}</div>
          </div>
          <div class="stat">
            <div class="stat__label">Active</div>
            <div class="stat__value">{{ activeTasks }}</div>
          </div>
          <div class="stat">
            <div class="stat__label">Completed</div>
            <div class="stat__value">{{ completedTasks }}</div>
          </div>
        </div>
      </section>

      <section class="task-list">
        <TaskItem
            v-for="task in filteredTasks"
            :key="task.id"
            :task="task"
            @toggle-complete="toggleComplete"
            @edit="editTask"
            @delete="deleteTask"
        />

        <div v-if="filteredTasks.length === 0" class="empty-state">
          <h3 class="empty-state__title">Aucune tâche</h3>
          <p class="empty-state__text">Essayez de modifier la recherche ou le filtre.</p>
        </div>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import TaskItem from './components/TaskItem.vue'
import AddTask from './components/AddTask.vue'
import SearchFilter from './components/SearchFilter.vue'
import StatusFilter from './components/StatusFilter.vue'

const tasks = ref([
  {
    id: 1,
    title: 'Learn Vue.js Components',
    description: 'Master component basics',
    completed: false,
    createdAt: '2026-01-20'
  },
  {
    id: 2,
    title: 'Understand Props',
    description: 'Learn how to pass data to components',
    completed: true,
    createdAt: '2026-01-21'
  }
])

const searchQuery = ref('')
const currentFilter = ref('all') // 'all', 'active', 'completed'

// Event Handlers
function addTask(task) {
  tasks.value.unshift(task)
}

function toggleComplete(taskId) {
  const task = tasks.value.find(t => t.id === taskId)
  if (task) {
    task.completed = !task.completed
  }
}

function editTask(taskId) {
  // Implement edit functionality
  const task = tasks.value.find(t => t.id === taskId)
  const newTitle = prompt('Edit task:', task.title)
  if (newTitle) {
    task.title = newTitle
  }
}

function deleteTask(taskId) {
  tasks.value = tasks.value.filter(t => t.id !== taskId)
}

function handleFilterChange(filter) {
  currentFilter.value = filter
}

// Computed Properties
const filteredTasks = computed(() => {
  let result = tasks.value

  // Apply search filter
  if (searchQuery.value) {
    result = result.filter(task =>
        task.title.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
        task.description.toLowerCase().includes(searchQuery.value.toLowerCase())
    )
  }

  // Apply status filter
  if (currentFilter.value === 'active') {
    result = result.filter(task => !task.completed)
  } else if (currentFilter.value === 'completed') {
    result = result.filter(task => task.completed)
  }

  return result
})

const activeTasks = computed(() =>
    tasks.value.filter(t => !t.completed).length
)

const completedTasks = computed(() =>
    tasks.value.filter(t => t.completed).length
)
</script>

<style scoped>
:global(:root) {
  --bg: #0b1220;
  --surface: rgba(255, 255, 255, 0.06);
  --surface-strong: rgba(255, 255, 255, 0.09);
  --text: rgba(255, 255, 255, 0.92);
  --muted: rgba(255, 255, 255, 0.68);
  --border: rgba(255, 255, 255, 0.12);
  --shadow: 0 10px 30px rgba(0, 0, 0, 0.35);
  --ring: 0 0 0 4px rgba(66, 184, 131, 0.18);
  --primary: #42b883; /* Vue green vibe */
  --primary-2: #2f9f6b;
  --danger: #ff5a6a;
  --warning: #ffcc66;
  --radius: 16px;
}

:global(body) {
  margin: 0;
  background:
      radial-gradient(1000px 600px at 20% -10%, rgba(66, 184, 131, 0.25), transparent 60%),
      radial-gradient(900px 500px at 100% 0%, rgba(120, 87, 255, 0.22), transparent 55%),
      var(--bg);
  color: var(--text);
  font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji",
  "Segoe UI Emoji";
}

:global(*),
:global(*::before),
:global(*::after) {
  box-sizing: border-box;
}

.app {
  min-height: 100vh;
}

.app-header {
  padding: 32px 16px 12px;
}

.app-header__inner {
  max-width: 980px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.app-title {
  margin: 0;
  letter-spacing: -0.02em;
  font-size: 28px;
  line-height: 1.1;
}

.app-subtitle {
  margin: 0;
  color: var(--muted);
  font-size: 14px;
}

.app-main {
  max-width: 980px;
  margin: 0 auto;
  padding: 16px;
  display: grid;
  gap: 16px;
}

.card {
  background: linear-gradient(180deg, var(--surface-strong), var(--surface));
  border: 1px solid var(--border);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  padding: 16px;
}

.card--filters {
  display: grid;
  gap: 14px;
}

.filters {
  display: grid;
  grid-template-columns: 1fr;
  gap: 12px;
}

@media (min-width: 720px) {
  .filters {
    grid-template-columns: 1.3fr 1fr;
    align-items: start;
  }
}

.task-stats {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 10px;
}

.stat {
  border: 1px solid var(--border);
  background: rgba(0, 0, 0, 0.12);
  border-radius: 14px;
  padding: 12px;
}

.stat__label {
  color: var(--muted);
  font-size: 12px;
}

.stat__value {
  margin-top: 4px;
  font-size: 18px;
  font-weight: 700;
}

.task-list {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.empty-state {
  border: 1px dashed rgba(255, 255, 255, 0.18);
  border-radius: var(--radius);
  padding: 18px;
  text-align: center;
  color: var(--muted);
  background: rgba(0, 0, 0, 0.10);
}

.empty-state__title {
  margin: 0 0 6px;
  color: var(--text);
  font-size: 16px;
}

.empty-state__text {
  margin: 0;
  font-size: 13px;
}
</style>