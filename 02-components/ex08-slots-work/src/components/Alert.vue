<!-- src/components/Alert.vue -->
<template>
  <div class="alert" :class="`alert--${type}`" role="status">
    <div class="icon">
      <slot name="icon">i</slot>
    </div>

    <div class="content">
      <slot>
        <p class="msg">Message</p>
      </slot>
    </div>

    <div v-if="$slots.actions" class="actions">
      <slot name="actions"></slot>
    </div>
  </div>
</template>

<script setup>
defineProps({
  type: { type: String, default: 'info' } // success, error, warning, info
})
</script>

<style scoped>
.alert{
  display:grid;
  grid-template-columns: auto 1fr auto;
  gap: 12px;
  align-items:center;
  padding: 12px 14px;
  border-radius: 14px;
  border: 1px solid var(--border);
  background: rgba(0,0,0,.12);
}
.icon{
  width: 34px; height: 34px;
  display:grid; place-items:center;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(255,255,255,.06);
  color: var(--text);
}
.msg{ margin:0; color: var(--text); }
.actions{ display:flex; gap: 8px; }

.alert--success{ border-color: rgba(66,184,131,.35); }
.alert--error{ border-color: rgba(255,90,106,.35); }
.alert--warning{ border-color: rgba(255,204,102,.35); }
.alert--info{ border-color: rgba(105,167,255,.35); }
</style>