<template>
  <div class="container">
    <header class="hero">
      <h1 class="hero__title">Slots Demo</h1>
      <p class="hero__subtitle">
        Default slots, named slots, scoped slots, fallback content — le tout en mode “Vue moderne”.
      </p>
      <p class="hero__hint">
        Astuce : essaie de supprimer certains <span class="kbd">#header</span> / <span class="kbd">#footer</span> pour voir les fallbacks.
      </p>
    </header>

    <PageLayout>
      <template #header>
        <div class="topbar">
          <strong>Component Library</strong>
          <span class="muted">Exercise 08</span>
        </div>
      </template>

      <template #sidebar>
        <nav class="nav">
          <a href="#cards">Cards</a>
          <a href="#users">UserList</a>
          <a href="#tabs">Tabs</a>
          <a href="#alerts">Alerts</a>
          <a href="#table">DataTable</a>
          <a href="#modal">Modal</a>
        </nav>
      </template>

      <section id="cards" class="stack">
        <h2 class="section-title">Cards</h2>

        <BaseCard>
          <p>Contenu custom via <strong>default slot</strong>.</p>
        </BaseCard>

        <Card>
          <template #header>
            <h3 class="h3">Mon header custom</h3>
          </template>

          <p>Contenu principal dans le slot par défaut.</p>

          <template #footer>
            <button class="btn">Action</button>
            <button class="btn btn--ghost">Cancel</button>
          </template>
        </Card>
      </section>

      <section id="users" class="stack">
        <h2 class="section-title">UserList (scoped slot)</h2>

        <UserList :users="users">
          <template #default="{ user, index }">
            <div class="user-custom">
              <span class="index">{{ index + 1 }}.</span>
              <img class="avatar" :src="user.avatar" :alt="user.name">
              <div class="meta">
                <div class="name">{{ user.name }}</div>
                <div class="role">{{ user.role }}</div>
              </div>
              <button class="btn btn--ghost" type="button" @click="editUser(user)">Edit</button>
            </div>
          </template>
        </UserList>
      </section>

      <section id="tabs" class="stack">
        <h2 class="section-title">Tabs</h2>

        <TabContainer v-model="activeTab">
          <template #label-Overview>Vue vibe</template>
          <template #label-Details>Détails</template>
          <template #label-API>API</template>

          <TabItem name="Overview" :active-name="activeTab">
            <p class="muted">Labels via named slots: <span class="kbd">#label-Overview</span>, etc.</p>
          </TabItem>

          <TabItem name="Details" :active-name="activeTab">
            <p>Les <strong>TabItem</strong> passent juste le contenu via slot.</p>
          </TabItem>

          <TabItem name="API" :active-name="activeTab">
            <p class="muted">Tu pourrais ajouter des props/évènements ici, mais l’exercice cible surtout les slots.</p>
          </TabItem>
        </TabContainer>
      </section>

      <section id="alerts" class="stack">
        <h2 class="section-title">Alert (named slots)</h2>

        <Alert type="success">
          <template #icon>✓</template>
          <p class="msg">Tout est OK. Slots + style propre.</p>
          <template #actions>
            <button class="btn btn--ghost" type="button">Undo</button>
          </template>
        </Alert>

        <Alert type="warning">
          <template #icon>!</template>
          <p class="msg">Attention : c’est un warning.</p>
        </Alert>
      </section>

      <section id="table" class="stack">
        <h2 class="section-title">DataTable (scoped slots)</h2>

        <DataTable :data="tableData" :columns="['name', 'email', 'status', 'actions']">
          <template #cell-status="{ value }">
            <span class="pill" :class="`pill--${value}`">{{ value }}</span>
          </template>

          <template #cell-actions="{ row }">
            <button class="btn btn--ghost" type="button" @click="editUser(row)">Edit</button>
            <button class="btn btn--danger" type="button" @click="deleteUser(row)">Delete</button>
          </template>

          <template #footer>
            <tr>
              <td colspan="4" class="tfoot">
                <span class="muted">Total lignes : {{ tableData.length }}</span>
              </td>
            </tr>
          </template>
        </DataTable>
      </section>

      <section id="modal" class="stack">
        <h2 class="section-title">Modal</h2>

        <div class="row">
          <button class="btn btn--primary" type="button" @click="modalOpen = true">
            Open Modal
          </button>
          <span class="muted">Overlay + slots title/footer + close event.</span>
        </div>

        <Modal :is-open="modalOpen" @close="modalOpen = false">
          <template #title>
            <h2>Confirm Action</h2>
          </template>

          <p>Es-tu sûr de vouloir continuer ?</p>

          <template #footer>
            <button class="btn btn--ghost" type="button" @click="modalOpen = false">Cancel</button>
            <button class="btn btn--primary" type="button" @click="confirmAction">Confirm</button>
          </template>
        </Modal>
      </section>

      <template #footer>
        <div class="footerbar">
          <span class="muted">Checklist : fallback, named slots, scoped slots, $slots, Teleport ✅</span>
        </div>
      </template>
    </PageLayout>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import BaseCard from './components/BaseCard.vue'
import Card from './components/Card.vue'
import UserList from './components/UserList.vue'
import Modal from './components/Modal.vue'
import DataTable from './components/DataTable.vue'
import PageLayout from './components/PageLayout.vue'
import Alert from './components/Alert.vue'
import TabContainer from './components/Tabs/TabContainer.vue'
import TabItem from './components/Tabs/TabItem.vue'

const modalOpen = ref(false)
const activeTab = ref('Overview')

const users = ref([
  { id: 1, name: 'John Doe', email: 'john@example.com', avatar: 'https://i.pravatar.cc/120?img=1', role: 'Developer' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com', avatar: 'https://i.pravatar.cc/120?img=2', role: 'Designer' }
])

const tableData = ref([
  { name: 'Alice', email: 'alice@example.com', status: 'active' },
  { name: 'Bob', email: 'bob@example.com', status: 'inactive' },
  { name: 'Charlie', email: 'charlie@example.com', status: 'active' }
])

function confirmAction() {
  alert('Action confirmed!')
  modalOpen.value = false
}

function editUser(user) {
  alert(`Editing: ${user.name}`)
}

function deleteUser(user) {
  alert(`Deleting: ${user.name}`)
}
</script>

<style scoped>
.hero{
  padding: 28px 0 10px;
  display:grid;
  gap: 8px;
}
.hero__title{
  margin: 0;
  font-size: 30px;
  letter-spacing: -0.02em;
}
.hero__subtitle{
  margin: 0;
  color: var(--muted);
  max-width: 70ch;
}
.hero__hint{
  margin: 0;
  color: rgba(255,255,255,.58);
  font-size: 13px;
}
.section-title{
  margin: 0;
  font-size: 16px;
  letter-spacing: -0.01em;
}
.stack{
  display:grid;
  gap: 12px;
  padding: 10px 0;
}
.topbar{
  display:flex;
  align-items:center;
  justify-content: space-between;
}
.footerbar{
  display:flex;
  justify-content: space-between;
}
.muted{ color: var(--muted); }

.nav{
  display:grid;
  gap: 8px;
}
.nav a{
  text-decoration:none;
  color: var(--muted);
  padding: 8px 10px;
  border-radius: 12px;
  border: 1px solid transparent;
}
.nav a:hover{
  color: var(--text);
  background: rgba(255,255,255,.05);
  border-color: var(--border);
}

.h3{ margin:0; font-size: 14px; }

.row{
  display:flex;
  gap: 12px;
  align-items:center;
  flex-wrap: wrap;
}

.btn{
  height: 38px;
  padding: 0 14px;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(255,255,255,.08);
  color: var(--text);
  cursor: pointer;
  transition: transform 120ms ease, background 120ms ease, border-color 120ms ease;
}
.btn:hover{ transform: translateY(-1px); background: rgba(255,255,255,.10); }
.btn:active{ transform: translateY(0); }
.btn--ghost{ background: transparent; }
.btn--primary{
  border-color: rgba(66,184,131,.35);
  background: linear-gradient(180deg, rgba(66,184,131,.25), rgba(66,184,131,.14));
}
.btn--danger{
  border-color: rgba(255,90,106,.35);
  background: linear-gradient(180deg, rgba(255,90,106,.22), rgba(255,90,106,.12));
}

.user-custom{
  display:flex;
  gap: 12px;
  align-items:center;
}
.index{ color: var(--muted); width: 26px; text-align:right; }
.avatar{
  width: 40px; height: 40px;
  border-radius: 12px;
  border: 1px solid var(--border);
}
.meta{ display:grid; gap: 2px; flex: 1; }
.name{ font-weight: 800; }
.role{ color: var(--muted); font-size: 13px; }

.pill{
  display:inline-flex;
  align-items:center;
  height: 26px;
  padding: 0 10px;
  border-radius: 999px;
  border: 1px solid var(--border);
  background: rgba(255,255,255,.06);
  font-size: 12px;
}
.pill--active{
  border-color: rgba(66,184,131,.35);
  background: rgba(66,184,131,.16);
}
.pill--inactive{
  border-color: rgba(255,204,102,.35);
  background: rgba(255,204,102,.14);
}
.tfoot{
  padding: 12px 14px;
}
.msg{ margin: 0; }
</style>