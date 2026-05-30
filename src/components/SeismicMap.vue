<template>
  <div class="relative rounded-xl overflow-hidden bg-[var(--surface-muted)]" style="height: 500px">
    <div class="absolute inset-0 flex items-center justify-center">
      <div class="text-center">
        <Map class="w-16 h-16 text-[var(--text-muted)] mx-auto mb-4" />
        <p class="text-[var(--text-muted)]">Seismic Map Visualization</p>
        <p class="text-sm text-[var(--text-muted)] mt-2">Interactive map will be displayed here</p>
        
        <!-- Эпицентр -->
        <div class="relative mt-8">
          <div class="w-8 h-8 bg-[var(--danger)] rounded-full animate-pulse mx-auto"></div>
          <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-24 h-24 border-2 border-[var(--danger)] rounded-full opacity-50"></div>
          <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 w-48 h-48 border border-[var(--warning)] rounded-full opacity-30"></div>
          <p class="text-sm text-[var(--text)] mt-4">Epicenter: 35.7°N, 51.4°E</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { Map } from 'lucide-vue-next'
</script>