<template>
  <div class="pt-[72px] p-6">
    <div class="max-w-7xl mx-auto space-y-6">
      <!-- Danger Hero -->
      <DangerHero level="RED" :confidence="94" />
      
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <!-- SHAP Analysis -->
        <div class="card">
          <h2 class="text-lg font-semibold text-[var(--text)] mb-4">SHAP-анализ факторов</h2>
          <ShapImpactChart />
        </div>
        
        <!-- Event Summary -->
        <div class="card">
          <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Сводка события</h2>
          <div class="space-y-3">
            <div class="flex justify-between py-2 border-b border-[var(--border)]">
              <span class="text-[var(--text-muted)]">Магнитуда</span>
              <span class="font-medium text-[var(--text)]">6.2</span>
            </div>
            <div class="flex justify-between py-2 border-b border-[var(--border)]">
              <span class="text-[var(--text-muted)]">Глубина</span>
              <span class="font-medium text-[var(--text)]">10 км</span>
            </div>
            <div class="flex justify-between py-2 border-b border-[var(--border)]">
              <span class="text-[var(--text-muted)]">Интенсивность MM (1)</span>
              <span class="font-medium text-[var(--text)]">VII</span>
            </div>
            <div class="flex justify-between py-2 border-b border-[var(--border)]">
              <span class="text-[var(--text-muted)]">Интенсивность MM (2)</span>
              <span class="font-medium text-[var(--text)]">VII</span>
            </div>
            <div class="flex justify-between py-2">
              <span class="text-[var(--text-muted)]">Значимость события</span>
              <span class="font-medium text-[var(--text)]">Критическая</span>
            </div>
          </div>
          
          <ConfidenceBar :confidence="94" level="RED" class="mt-6" />
        </div>
      </div>
      
      <!-- Operational Recommendations -->
      <div class="card">
        <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Рекомендации для оператора</h2>
        <RecommendationPanel />
      </div>
      
      <!-- Impact Zone Map -->
      <div class="card">
        <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Карта зоны поражения</h2>
        <div class="h-64 bg-[var(--surface-muted)] rounded-xl flex items-center justify-center">
          <p class="text-[var(--text-muted)]">Визуализация зоны поражения</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import DangerHero from '../components/DangerHero.vue'
import ShapImpactChart from '../components/ShapImpactChart.vue'
import ConfidenceBar from '../components/ConfidenceBar.vue'
import RecommendationPanel from '../components/RecommendationPanel.vue'
</script>