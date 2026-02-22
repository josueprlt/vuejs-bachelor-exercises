<!-- src/components/TabContainer.vue -->
<template>
  <div class="tabs">
    <div class="tabs-nav" role="tablist">
      <button
          v-for="tab in tabs"
          :key="tab.name"
          type="button"
          class="tab-btn"
          :class="{ active: tab.name === modelValue }"
          @click="$emit('update:modelValue', tab.name)"
          role="tab"
          :aria-selected="tab.name === modelValue"
      >
        <component :is="tab.labelSlot" v-if="tab.labelSlot" />
        <span v-else>{{ tab.name }}</span>
      </button>
    </div>

    <div class="tabs-body">
      <slot />
    </div>
  </div>
</template>

<script setup>
import { provide, ref, computed, useSlots, h } from 'vue'

const props = defineProps({
  modelValue: { type: String, required: true }
})
defineEmits(['update:modelValue'])

const slots = useSlots()
const items = ref([])

provide('tabsRegister', (tab) => {
  if (!items.value.some(t => t.name === tab.name)) items.value.push(tab)
})

const tabs = computed(() => {
  return items.value.map(t => {
    const slotName = `label-${t.name}`
    const labelSlot = slots[slotName] ? () => h('span', slots[slotName]()) : null
    return { ...t, labelSlot }
  })
})
</script>

<style scoped>
.tabs{
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: linear-gradient(180deg, var(--surface-2), var(--surface));
  box-shadow: var(--shadow);
  overflow: hidden;
}
.tabs-nav{
  display:flex;
  gap: 8px;
  padding: 10px;
  border-bottom: 1px solid var(--border);
  background: rgba(0,0,0,.14);
}
.tab-btn{
  height: 36px;
  padding: 0 12px;
  border-radius: 12px;
  border: 1px solid transparent;
  background: transparent;
  color: var(--muted);
  cursor: pointer;
}
.tab-btn.active{
  color: var(--text);
  border-color: rgba(66,184,131,.35);
  background: rgba(66,184,131,.16);
}
.tabs-body{ padding: 16px; }
</style>