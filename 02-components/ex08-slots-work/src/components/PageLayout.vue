<!-- src/components/PageLayout.vue -->
<template>
  <div class="layout">
    <header class="header">
      <slot name="header">
        <div class="header-default">Header</div>
      </slot>
    </header>

    <div class="body">
      <aside class="sidebar">
        <slot name="sidebar">
          <div class="muted">Sidebar</div>
        </slot>
      </aside>

      <main class="main">
        <slot />
      </main>
    </div>

    <footer class="footer">
      <slot name="footer">
        <div class="muted">Footer</div>
      </slot>
    </footer>
  </div>
</template>

<style scoped>
.layout{
  display:grid;
  gap: 12px;
}
.header, .footer{
  padding: 14px 16px;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: linear-gradient(180deg, var(--surface-2), var(--surface));
  box-shadow: var(--shadow);
}
.body{
  display:grid;
  grid-template-columns: 1fr;
  gap: 12px;
}
@media (min-width: 860px){
  .body{ grid-template-columns: 280px 1fr; align-items:start; }
}
.sidebar, .main{
  padding: 16px;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: rgba(0,0,0,.12);
}
.muted{ color: var(--muted); }
.header-default{ font-weight: 800; letter-spacing: -0.01em; }
</style>