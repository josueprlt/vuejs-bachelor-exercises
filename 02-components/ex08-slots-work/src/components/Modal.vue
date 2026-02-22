<!-- src/components/Modal.vue -->
<template>
  <Teleport to="body">
    <Transition name="modal">
      <div v-if="isOpen" class="overlay" @click="$emit('close')" role="dialog" aria-modal="true">
        <div class="modal" @click.stop>
          <header class="modal-header">
            <div class="modal-title">
              <slot name="title">
                <h2>Modal Title</h2>
              </slot>
            </div>

            <button class="icon-btn" type="button" @click="$emit('close')" aria-label="Fermer">
              ×
            </button>
          </header>

          <div class="modal-body">
            <slot>
              <p class="muted">Modal content</p>
            </slot>
          </div>

          <footer class="modal-footer">
            <slot name="footer">
              <button class="btn" type="button" @click="$emit('close')">Close</button>
            </slot>
          </footer>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
defineProps({
  isOpen: { type: Boolean, default: false }
})
defineEmits(['close'])
</script>

<style scoped>
.overlay{
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,.55);
  display: grid;
  place-items: center;
  padding: 18px;
  z-index: 1000;
}
.modal{
  width: min(560px, 100%);
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: linear-gradient(180deg, rgba(20,26,40,.98), rgba(10,14,24,.96));
  box-shadow: 0 30px 80px rgba(0,0,0,.55);
  overflow: hidden;
}
.modal-header{
  display:flex;
  align-items:center;
  justify-content: space-between;
  gap: 12px;
  padding: 14px 16px;
  border-bottom: 1px solid var(--border);
}
.modal-title :deep(h2){
  margin: 0;
  font-size: 16px;
  letter-spacing: -0.01em;
}
.icon-btn{
  width: 36px;
  height: 36px;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(255,255,255,.06);
  color: var(--text);
  cursor: pointer;
}
.modal-body{ padding: 16px; }
.modal-footer{
  padding: 14px 16px;
  border-top: 1px solid var(--border);
  display:flex;
  justify-content:flex-end;
  gap: 10px;
}
.muted{ margin: 0; color: var(--muted); }

.btn{
  height: 38px;
  padding: 0 14px;
  border-radius: 12px;
  border: 1px solid var(--border);
  background: rgba(255,255,255,.08);
  color: var(--text);
  cursor: pointer;
}

.modal-enter-active, .modal-leave-active{ transition: opacity .18s ease; }
.modal-enter-from, .modal-leave-to{ opacity: 0; }
</style>