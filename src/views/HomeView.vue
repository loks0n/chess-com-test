<script setup lang="ts">
import CheckeredBoard from '@/components/board/CheckeredBoard.vue'
import HistoryList from '@/components/history/HistoryList.vue'
</script>

<script lang="ts">
import { ref } from 'vue'

const history = ref<number[]>([])

function addToHistory(square: number) {
  history.value.push(square)
}
</script>

<template>
  <div class="container">
    <main class="board-container">
      <CheckeredBoard @select="($square) => addToHistory($square)" />
    </main>
    <div class="mobile-only"><HistoryList :history="history" /></div>
    <div class="desktop-only"><HistoryList :history="history" vertical /></div>
  </div>
</template>

<style scoped>
.container {
  margin: 2em;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

@media (min-width: 768px) {
  .container {
    flex-direction: row;
    max-height: min(80dvh, 80dvw);
  }

  .board-container {
    flex: 0 1 min(80dvh, 80dvw);
  }
}
</style>
