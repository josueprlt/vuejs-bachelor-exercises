<!-- src/components/Card.vue -->
<template>
  <section class="card-shell">
    <header class="card-header">
      <slot name="header">
        <h3 class="title">Card Title</h3>
      </slot>
    </header>

    <div class="card-body">
      <slot>
        <p class="muted">Card content goes here</p>
      </slot>
    </div>

    <footer v-if="$slots.footer" class="card-footer">
      <slot name="footer"></slot>
    </footer>
  </section>
</template>

<style scoped>
.card-shell{
  border-radius: var(--radius);
  border: 1px solid var(--border);
  overflow: hidden;
  background: linear-gradient(180deg, var(--surface-2), var(--surface));
  box-shadow: var(--shadow);
}
.card-header, .card-footer{
  padding: 14px 16px;
  background: rgba(0,0,0,.14);
  border-bottom: 1px solid var(--border);
}
.card-footer{
  border-bottom: none;
  border-top: 1px solid var(--border);
}
.card-body{ padding: 16px; }
.title{ margin: 0; font-size: 14px; letter-spacing: -0.01em; }
.muted{ margin: 0; color: var(--muted); }
</style>