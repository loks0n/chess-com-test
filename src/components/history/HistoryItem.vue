<script lang="ts" setup>
const props = defineProps<{ square: number }>()
</script>

<template>
  <div class="history-item">
    {{ props.square }}
  </div>
</template>

<style scoped>
.history-item {
  display: grid;
  place-items: center;
  background-color: lightgreen;
  border-radius: 0.5em;
  padding: 0.5em;
  min-width: 3em;
  color: darkslategray;
  font-family: monospace;
  font-size: 1.5rem;
}
</style>
