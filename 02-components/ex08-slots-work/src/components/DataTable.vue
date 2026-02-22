<!-- src/components/DataTable.vue -->
<template>
  <div class="wrap">
    <table class="table">
      <thead>
      <tr>
        <th v-for="column in columns" :key="column">
          <slot :name="`header-${column}`" :column="column">
            {{ column }}
          </slot>
        </th>
      </tr>
      </thead>

      <tbody>
      <tr v-for="(row, index) in data" :key="index">
        <td v-for="column in columns" :key="column">
          <slot
              :name="`cell-${column}`"
              :row="row"
              :column="column"
              :value="row[column]"
          >
            {{ row[column] }}
          </slot>
        </td>
      </tr>
      </tbody>

      <tfoot v-if="$slots.footer">
      <slot name="footer"></slot>
      </tfoot>
    </table>
  </div>
</template>

<script setup>
defineProps({
  data: { type: Array, required: true },
  columns: { type: Array, required: true }
})
</script>

<style scoped>
.wrap{
  border-radius: var(--radius);
  border: 1px solid var(--border);
  overflow: hidden;
  background: rgba(0,0,0,.12);
}
.table{
  width: 100%;
  border-collapse: collapse;
}
th, td{
  padding: 12px 14px;
  border-bottom: 1px solid var(--border);
  text-align:left;
  font-size: 13px;
}
thead th{
  background: rgba(0,0,0,.18);
  color: var(--muted);
  font-weight: 600;
  letter-spacing: .01em;
}
tbody tr:hover td{
  background: rgba(255,255,255,.04);
}
</style>