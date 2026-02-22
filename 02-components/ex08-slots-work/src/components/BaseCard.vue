<!-- src/components/BaseCard.vue -->
<template>
  <section class="base-card">
    <slot>
      <p class="empty">Aucun contenu fourni</p>
    </slot>
  </section>
</template>

<style scoped>
.base-card{
  padding: 16px;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: linear-gradient(180deg, var(--surface-2), var(--surface));
  box-shadow: var(--shadow);
}
.empty{
  margin: 0;
  color: var(--muted);
  font-size: 13px;
}
</style>