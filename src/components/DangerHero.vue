<template>
  <div :class="['rounded-2xl p-8 text-white', heroClass]">
    <div class="flex items-center justify-between flex-wrap gap-4">
      <div>
        <div class="text-sm font-medium opacity-90 mb-2">{{ level }} LEVEL</div>
        <div class="text-6xl md:text-7xl font-bold">{{ title }}</div>
        <div class="text-lg opacity-90 mt-2">{{ description }}</div>
      </div>
      <div class="text-right">
        <div class="text-5xl font-bold">{{ confidence }}%</div>
        <div class="text-sm opacity-80">confidence</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  level: {
    type: String,
    default: 'RED'
  },
  confidence: {
    type: Number,
    default: 94
  }
})

const heroClass = computed(() => {
  if (props.level === 'RED') return 'danger-hero-red'
  if (props.level === 'ORANGE') return 'danger-hero-orange'
  if (props.level === 'YELLOW') return 'danger-hero-yellow'
  return 'danger-hero-green'
})

const title = computed(() => {
  if (props.level === 'RED') return 'КРАСНЫЙ УРОВЕНЬ ОПАСНОСТИ'
  if (props.level === 'ORANGE') return 'ОРАНЖЕВЫЙ УРОВЕНЬ ОПАСНОСТИ'
  if (props.level === 'YELLOW') return 'ЖЁЛТЫЙ УРОВЕНЬ ОПАСНОСТИ'
  return 'ЗЕЛЁНЫЙ УРОВЕНЬ ОПАСНОСТИ'
})

const description = computed(() => {
  if (props.level === 'RED') return 'Высокая вероятность разрушений и угрозы жизни'
  if (props.level === 'ORANGE') return 'Значительный риск, требуется подготовка'
  if (props.level === 'YELLOW') return 'Средний риск, мониторинг ситуации'
  return 'Незначительный риск, штатный режим'
})
</script>