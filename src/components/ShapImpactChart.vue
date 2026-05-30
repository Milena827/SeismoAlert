<template>
  <div class="space-y-4">
    <div v-for="factor in factors" :key="factor.name" class="space-y-1">
      <div class="flex justify-between text-sm">
        <span class="text-[var(--text-secondary)]">{{ factor.name }}</span>
        <span class="font-bold" :class="getFactorColor(factor.influence)">{{ factor.influence }}%</span>
      </div>
      <div class="h-2 bg-[var(--surface-muted)] rounded-full overflow-hidden">
        <div 
          class="h-full rounded-full transition-all duration-500"
          :class="getBarColor(factor.influence)"
          :style="{ width: `${factor.influence}%` }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup>
const factors = [
  { name: 'Magnitude 6.2', influence: 42 },
  { name: 'Depth 10 km', influence: 31 },
  { name: 'MM Intensity', influence: 18 },
  { name: 'Event Significance', influence: 9 }
]

const getFactorColor = (influence) => {
  if (influence >= 40) return 'text-[var(--danger)]'
  if (influence >= 30) return 'text-[var(--warning)]'
  return 'text-[var(--text-muted)]'
}

const getBarColor = (influence) => {
  if (influence >= 40) return 'bg-[var(--danger)]'
  if (influence >= 30) return 'bg-[var(--warning)]'
  return 'bg-[var(--secondary)]'
}
</script>