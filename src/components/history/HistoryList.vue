<script lang="ts" setup>
import { ref, watch, nextTick, type PropType } from 'vue'
import HistoryItem from './HistoryItem.vue'

const props = defineProps({
  vertical: {
    type: Boolean as PropType<boolean>,
    default: false
  },
  history: {
    type: Array as PropType<number[]>,
    required: true
  }
})

const historyEl = ref<HTMLDivElement | null>(null)

function scrollToElement() {
  const el = historyEl.value
  if (el) {
    el.scroll({ top: el.scrollHeight, left: el.scrollWidth, behavior: 'smooth' })
  }
}

watch(
  props.history,
  async () => {
    await nextTick()
    scrollToElement()
  },
  { deep: true }
)
</script>

<template>
  <div class="history" ref="historyEl" :class="{ vertical }">
    <template v-for="square in history" :key="square">
      <HistoryItem :square="square" />
    </template>
  </div>
</template>

<style scoped>
.history {
  display: flex;
  gap: 0.5em;
  padding: 1em 0;
  overflow-x: auto;
  overflow-y: none;
  max-width: 100%;
  max-height: 100%;
}

.vertical {
  flex-direction: column;
  overflow-x: none;
  overflow-y: auto;
  padding: 0 1em;
}
</style>
