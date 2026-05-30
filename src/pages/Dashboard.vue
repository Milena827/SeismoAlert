<template>
  <div class="pt-[72px] p-6">
    <div class="max-w-7xl mx-auto space-y-6">
      <!-- Seismic Map -->
      <SeismicMap />
      
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Input Panel -->
        <div class="lg:col-span-1">
          <div class="card">
            <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Параметры события</h2>
            
            <div class="space-y-4">
              <div>
                <label class="block text-sm font-medium text-[var(--text-secondary)] mb-1">Магнитуда</label>
                <input type="range" v-model="magnitude" min="0" max="10" step="0.1" class="w-full" />
                <div class="text-right text-sm text-[var(--text-muted)] mt-1">{{ magnitude }}</div>
              </div>
              
              <div>
                <label class="block text-sm font-medium text-[var(--text-secondary)] mb-1">Глубина (км)</label>
                <input type="range" v-model="depth" min="0" max="700" step="1" class="w-full" />
                <div class="text-right text-sm text-[var(--text-muted)] mt-1">{{ depth }}</div>
              </div>
              
              <div>
                <label class="block text-sm font-medium text-[var(--text-secondary)] mb-1">Интенсивность MM (1)</label>
                <select v-model="mm1" class="w-full px-3 py-2 rounded-lg bg-[var(--surface-muted)] border border-[var(--border)] text-[var(--text)]">
                  <option v-for="i in ['I','II','III','IV','V','VI','VII','VIII','IX','X','XI','XII']" :key="i">{{ i }}</option>
                </select>
              </div>
              
              <div>
                <label class="block text-sm font-medium text-[var(--text-secondary)] mb-1">Интенсивность MM (2)</label>
                <select v-model="mm2" class="w-full px-3 py-2 rounded-lg bg-[var(--surface-muted)] border border-[var(--border)] text-[var(--text)]">
                  <option v-for="i in ['I','II','III','IV','V','VI','VII','VIII','IX','X','XI','XII']" :key="i">{{ i }}</option>
                </select>
              </div>
              
              <div>
                <label class="block text-sm font-medium text-[var(--text-secondary)] mb-1">Значимость события</label>
                <select v-model="significance" class="w-full px-3 py-2 rounded-lg bg-[var(--surface-muted)] border border-[var(--border)] text-[var(--text)]">
                  <option>Низкая</option>
                  <option>Средняя</option>
                  <option>Высокая</option>
                  <option>Критическая</option>
                </select>
              </div>
              
              <button @click="analyze" class="w-full py-3 bg-[var(--primary)] text-white rounded-lg font-medium hover:bg-[var(--primary)]/90 transition">
                Анализировать событие
              </button>
            </div>
          </div>
        </div>
        
        <!-- Recent Events -->
        <div class="lg:col-span-2">
          <div class="card">
            <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Последние события</h2>
            <div class="space-y-3">
              <div v-for="event in recentEvents" :key="event.id" class="flex items-center justify-between p-3 rounded-lg bg-[var(--surface-muted)]">
                <div>
                  <span class="font-mono text-sm text-[var(--text)]">{{ event.mag }}</span>
                  <p class="text-xs text-[var(--text-muted)]">{{ event.date }}</p>
                </div>
                <span :class="getEventBadgeClass(event.level)" class="px-3 py-1 rounded-full text-xs font-medium">
                  {{ getLevelText(event.level) }}
                </span>
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
import SeismicMap from '../components/SeismicMap.vue'

const router = useRouter()
const magnitude = ref(6.2)
const depth = ref(10)
const mm1 = ref('VII')
const mm2 = ref('VII')
const significance = ref('Критическая')

const recentEvents = ref([
  { id: 1, mag: 'M6.2', level: 'RED', date: '2025-01-15 14:32' },
  { id: 2, mag: 'M5.8', level: 'ORANGE', date: '2025-01-14 09:17' },
  { id: 3, mag: 'M4.3', level: 'YELLOW', date: '2025-01-13 22:45' },
  { id: 4, mag: 'M3.1', level: 'GREEN', date: '2025-01-12 11:03' }
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

const getEventBadgeClass = (level) => {
  const classes = {
    RED: 'bg-[var(--danger)]/10 text-[var(--danger)]',
    ORANGE: 'bg-[var(--warning)]/10 text-[var(--warning)]',
    YELLOW: 'bg-[var(--caution)]/10 text-[var(--caution)]',
    GREEN: 'bg-[var(--safe)]/10 text-[var(--safe)]'
  }
  return classes[level] || ''
}

const analyze = () => {
  router.push('/results')
}
</script>