<template>
  <div class="pt-[72px] p-6">
    <div class="max-w-4xl mx-auto">
      <h1 class="text-3xl font-bold text-[var(--text)] mb-2">Хронология событий</h1>
      <p class="text-[var(--text-muted)] mb-8">История сейсмических событий</p>
      
      <div class="relative">
        <div class="absolute left-6 top-0 bottom-0 w-px bg-[var(--border)]"></div>
        
        <div v-for="(event, index) in timelineEvents" :key="event.id" class="relative pl-16 pb-8 last:pb-0">
          <div class="absolute left-0 top-0 w-12 h-12 rounded-full flex items-center justify-center" :class="getEventBgClass(event.level)">
            <span class="font-bold text-sm">{{ event.year }}</span>
          </div>
          
          <div class="card cursor-pointer hover:shadow-lg transition" @click="viewEvent(event)">
            <div class="flex items-center justify-between flex-wrap gap-4">
              <div>
                <span class="text-xl font-mono font-bold text-[var(--text)]">{{ event.magnitude }}</span>
                <p class="text-sm text-[var(--text-muted)] mt-1">{{ event.date }}</p>
              </div>
              <span :class="getEventBadgeClass(event.level)" class="px-4 py-1.5 rounded-full text-sm font-medium">
                {{ getLevelText(event.level) }}
              </span>
              <div class="text-right">
                <div class="text-lg font-bold" :class="getEventTextClass(event.level)">{{ event.confidence }}%</div>
                <div class="text-xs text-[var(--text-muted)]">уверенность</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const timelineEvents = ref([
  { id: 1, year: '2025', magnitude: 'M6.2', level: 'RED', confidence: 94, date: '15 января 2025' },
  { id: 2, year: '2025', magnitude: 'M5.7', level: 'ORANGE', confidence: 89, date: '14 января 2025' },
  { id: 3, year: '2025', magnitude: 'M4.4', level: 'YELLOW', confidence: 81, date: '13 января 2025' },
  { id: 4, year: '2025', magnitude: 'M3.0', level: 'GREEN', confidence: 76, date: '12 января 2025' }
])

const getLevelText = (level) => {
  const texts = {
    RED: 'КРАСНЫЙ',
    ORANGE: 'ОРАНЖЕВЫЙ',
    YELLOW: 'ЖЁЛТЫЙ',
    GREEN: 'ЗЕЛЁНЫЙ'
  }
  return texts[level] || ''
}

const getEventBgClass = (level) => {
  const classes = {
    RED: 'bg-[var(--danger)]/20 text-[var(--danger)]',
    ORANGE: 'bg-[var(--warning)]/20 text-[var(--warning)]',
    YELLOW: 'bg-[var(--caution)]/20 text-[var(--caution)]',
    GREEN: 'bg-[var(--safe)]/20 text-[var(--safe)]'
  }
  return classes[level] || ''
}

const getEventBadgeClass = (level) => {
  const classes = {
    RED: 'bg-[var(--danger)]/10 text-[var(--danger)] border border-[var(--danger)]/20',
    ORANGE: 'bg-[var(--warning)]/10 text-[var(--warning)] border border-[var(--warning)]/20',
    YELLOW: 'bg-[var(--caution)]/10 text-[var(--caution)] border border-[var(--caution)]/20',
    GREEN: 'bg-[var(--safe)]/10 text-[var(--safe)] border border-[var(--safe)]/20'
  }
  return classes[level] || ''
}

const getEventTextClass = (level) => {
  const classes = {
    RED: 'text-[var(--danger)]',
    ORANGE: 'text-[var(--warning)]',
    YELLOW: 'text-[var(--caution)]',
    GREEN: 'text-[var(--safe)]'
  }
  return classes[level] || ''
}

const viewEvent = (event) => {
  router.push('/results')
}
</script>