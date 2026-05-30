<template>
  <div class="space-y-3">
    <div v-for="(rec, index) in recommendations" :key="index" class="flex items-start gap-3">
      <div class="w-6 h-6 rounded-full bg-[var(--primary)]/10 flex items-center justify-center flex-shrink-0 mt-0.5">
        <Check class="w-3 h-3 text-[var(--primary)]" />
      </div>
      <p class="text-[var(--text-secondary)]">{{ rec }}</p>
    </div>
  </div>
</template>

<script setup>
import { Check } from 'lucide-vue-next'

const recommendations = [
  'Усилить мониторинг региона',
  'Подготовить аварийно-спасательные подразделения',
  'Проверить состояние критической инфраструктуры',
  'Уведомить региональные органы управления'
]
</script>