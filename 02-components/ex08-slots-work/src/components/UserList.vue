<!-- src/components/UserList.vue -->
<template>
  <div class="list">
    <div v-for="(user, index) in users" :key="user.id" class="item">
      <slot :user="user" :index="index">
        <div class="default">
          <img class="avatar" :src="user.avatar" :alt="user.name">
          <div class="meta">
            <div class="name">{{ user.name }}</div>
            <div class="email">{{ user.email }}</div>
          </div>
        </div>
      </slot>
    </div>
  </div>
</template>

<script setup>
defineProps({
  users: { type: Array, required: true }
})
</script>

<style scoped>
.list{ display:flex; flex-direction:column; gap: 10px; }
.item{
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 12px;
  background: rgba(0,0,0,.12);
}
.default{ display:flex; gap: 12px; align-items:center; }
.avatar{
  width: 40px; height: 40px;
  border-radius: 12px;
  border: 1px solid var(--border);
}
.meta{ display:grid; gap: 2px; }
.name{ font-weight: 700; }
.email{ color: var(--muted); font-size: 13px; }
</style>