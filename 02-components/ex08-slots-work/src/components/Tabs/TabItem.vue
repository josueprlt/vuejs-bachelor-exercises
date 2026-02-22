<!-- src/components/TabItem.vue -->
<template>
  <section v-show="active" class="tab-panel" role="tabpanel">
    <slot />
  </section>
</template>

<script setup>
import { computed, inject, onMounted } from 'vue'

const props = defineProps({
  name: { type: String, required: true },
  activeName: { type: String, required: true }
})

const register = inject('tabsRegister', null)

onMounted(() => {
  register?.({ name: props.name })
})

const active = computed(() => props.name === props.activeName)
</script>

<style scoped>
.tab-panel{ color: var(--text); }
</style>