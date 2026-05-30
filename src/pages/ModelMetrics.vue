<template>
  <div class="pt-[72px] p-6">
    <div class="max-w-6xl mx-auto space-y-6">
      <h1 class="text-3xl font-bold text-[var(--text)]">Метрики модели</h1>
      <p class="text-[var(--text-muted)]">Оценка качества модели XGBoost для прогнозирования сейсмической опасности</p>
      
      <!-- Metrics Grid -->
      <div class="grid grid-cols-2 md:grid-cols-5 gap-4">
        <div class="card text-center">
          <p class="text-sm text-[var(--text-muted)] mb-2">Точность</p>
          <p class="text-2xl font-bold text-[var(--text)]">93.5%</p>
        </div>
        <div class="card text-center">
          <p class="text-sm text-[var(--text-muted)] mb-2">Полнота</p>
          <p class="text-2xl font-bold text-[var(--text)]">94.2%</p>
        </div>
        <div class="card text-center">
          <p class="text-sm text-[var(--text-muted)] mb-2">Чувствительность</p>
          <p class="text-2xl font-bold text-[var(--text)]">93.1%</p>
        </div>
        <div class="card text-center">
          <p class="text-sm text-[var(--text-muted)] mb-2">F1-мера</p>
          <p class="text-2xl font-bold text-[var(--text)]">93.6%</p>
        </div>
        <div class="card text-center">
          <p class="text-sm text-[var(--text-muted)] mb-2">ROC-AUC</p>
          <p class="text-2xl font-bold text-[var(--text)]">0.97</p>
        </div>
      </div>
      
      <!-- Confusion Matrix -->
      <div class="card">
        <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Матрица ошибок</h2>
        <div class="overflow-x-auto">
          <div class="grid grid-cols-5 gap-1 text-center">
            <div class="p-2"></div>
            <div class="p-2 text-sm font-medium text-[var(--text)]">ЗЕЛЁНЫЙ</div>
            <div class="p-2 text-sm font-medium text-[var(--text)]">ЖЁЛТЫЙ</div>
            <div class="p-2 text-sm font-medium text-[var(--text)]">ОРАНЖЕВЫЙ</div>
            <div class="p-2 text-sm font-medium text-[var(--text)]">КРАСНЫЙ</div>
            
            <div class="p-2 text-sm font-medium text-[var(--text)]">ЗЕЛЁНЫЙ</div>
            <div class="p-2 bg-[var(--safe)]/20 text-[var(--safe)] font-bold">2,847</div>
            <div class="p-2 bg-[var(--caution)]/10 text-[var(--caution)]">156</div>
            <div class="p-2 bg-[var(--warning)]/10 text-[var(--warning)]">12</div>
            <div class="p-2 bg-[var(--danger)]/10 text-[var(--danger)]">3</div>
            
            <div class="p-2 text-sm font-medium text-[var(--text)]">ЖЁЛТЫЙ</div>
            <div class="p-2 bg-[var(--safe)]/10">89</div>
            <div class="p-2 bg-[var(--caution)]/20 text-[var(--caution)] font-bold">3,921</div>
            <div class="p-2 bg-[var(--warning)]/10">234</div>
            <div class="p-2 bg-[var(--danger)]/10">12</div>
            
            <div class="p-2 text-sm font-medium text-[var(--text)]">ОРАНЖЕВЫЙ</div>
            <div class="p-2 bg-[var(--safe)]/10">8</div>
            <div class="p-2 bg-[var(--caution)]/10">167</div>
            <div class="p-2 bg-[var(--warning)]/20 text-[var(--warning)] font-bold">2,891</div>
            <div class="p-2 bg-[var(--danger)]/10">45</div>
            
            <div class="p-2 text-sm font-medium text-[var(--text)]">КРАСНЫЙ</div>
            <div class="p-2 bg-[var(--safe)]/10">2</div>
            <div class="p-2 bg-[var(--caution)]/10">23</div>
            <div class="p-2 bg-[var(--warning)]/10">178</div>
            <div class="p-2 bg-[var(--danger)]/20 text-[var(--danger)] font-bold">2,847</div>
          </div>
        </div>
        <div class="mt-4 p-3 bg-[var(--surface-muted)] rounded-lg">
          <p class="text-sm text-[var(--text-secondary)]">
            ✓ Модель практически не генерирует ложных красных тревог<br>
            ✓ Около 6% красных событий классифицируются как оранжевые (допустимый риск)
          </p>
        </div>
      </div>
      
      <!-- Feature Importance -->
      <div class="card">
        <h2 class="text-lg font-semibold text-[var(--text)] mb-4">Глобальная важность признаков</h2>
        <div class="space-y-3">
          <div v-for="feature in features" :key="feature.name">
            <div class="flex justify-between text-sm mb-1">
              <span class="text-[var(--text-secondary)]">{{ feature.name }}</span>
              <span class="text-[var(--text)]">{{ feature.importance }}%</span>
            </div>
            <div class="h-2 bg-[var(--surface-muted)] rounded-full overflow-hidden">
              <div class="h-full bg-[var(--primary)] rounded-full" :style="{ width: `${feature.importance}%` }"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const features = [
  { name: 'Магнитуда', importance: 42 },
  { name: 'Глубина', importance: 28 },
  { name: 'Интенсивность MM', importance: 18 },
  { name: 'Значимость события', importance: 12 }
]
</script>