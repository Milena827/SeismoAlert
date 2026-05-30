<template>
  <div class="space-y-2">
    <div class="flex justify-between text-sm">
      <span class="text-[var(--text-secondary)]">Model Confidence</span>
      <span class="font-bold" :class="confidenceColor">{{ confidence }}%</span>
    </div>
    <div class="h-3 bg-[var(--surface-muted)] rounded-full overflow-hidden">
      <div 
        class="h-full rounded-full transition-all duration-700"
        :class="confidenceBarClass"
        :style="{ width: `${confidence}%` }"
      ></div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  confidence: {
    type: Number,
    default: 94
  },
  level: {
    type: String,
    default: 'RED'
  }
})

const confidenceColor = computed(() => {
  if (props.level === 'RED') return 'text-[var(--danger)]'
  if (props.level === 'ORANGE') return 'text-[var(--warning)]'
  if (props.level === 'YELLOW') return 'text-[var(--caution)]'
  return 'text-[var(--safe)]'
})

const confidenceBarClass = computed(() => {
  if (props.level === 'RED') return 'bg-[var(--danger)]'
  if (props.level === 'ORANGE') return 'bg-[var(--warning)]'
  if (props.level === 'YELLOW') return 'bg-[var(--caution)]'
  return 'bg-[var(--safe)]'
})
</script>