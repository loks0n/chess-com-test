<script lang="ts" setup>
import { ref } from 'vue'

const emit = defineEmits<{
  (e: 'select', square: number): void
}>()

const selectedSquare = ref<number | null>(null)

const setSelected = (square: number) => {
  selectedSquare.value = square
  emit('select', square)
}
</script>

<template>
  <div class="checkered-board">
    <template v-for="i in 64" :key="i">
      <div
        class="checkered-square"
        :class="{ selected: selectedSquare === i }"
        @click="() => setSelected(i)"
      ></div>
    </template>
  </div>
</template>

<style scoped>
.checkered-board {
  display: grid;
  aspect-ratio: 1/1;
  grid-template: repeat(8, 1fr) / repeat(8, 1fr);
  background-color: antiquewhite;
  border-radius: 0.5em;
  overflow: hidden;
}

.checkered-square:nth-child(16n + 2),
.checkered-square:nth-child(16n + 4),
.checkered-square:nth-child(16n + 6),
.checkered-square:nth-child(16n + 8),
.checkered-square:nth-child(16n + 9),
.checkered-square:nth-child(16n + 11),
.checkered-square:nth-child(16n + 13),
.checkered-square:nth-child(16n + 15) {
  background-color: darkslategray;
}
.selected {
  border: 0.5em solid lightgreen;
  transition: border 0.1s;
}
</style>
