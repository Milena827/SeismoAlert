<template>
  <header class="fixed top-0 left-0 right-0 h-[72px] bg-[var(--surface)] border-b border-[var(--border)] px-6 flex items-center justify-between z-50">
    <div class="flex items-center gap-8">
      <div>
        <h1 class="text-xl font-bold text-[var(--danger)]">SeismoAlert</h1>
        <p class="text-xs text-[var(--text-muted)]">Система оценки сейсмической опасности</p>
      </div>
      
      <nav class="hidden md:flex gap-6">
        <router-link to="/" class="text-[var(--text-secondary)] hover:text-[var(--primary)] transition">Главная</router-link>
        <router-link to="/history" class="text-[var(--text-secondary)] hover:text-[var(--primary)] transition">История</router-link>
        <router-link to="/metrics" class="text-[var(--text-secondary)] hover:text-[var(--primary)] transition">Метрики модели</router-link>
      </nav>
    </div>
    
    <div class="flex items-center gap-4">
      <button @click="toggleTheme" class="p-2 rounded-lg bg-[var(--surface-muted)]">
        <Sun v-if="isDark" class="w-5 h-5 text-[var(--text-secondary)]" />
        <Moon v-else class="w-5 h-5 text-[var(--text-secondary)]" />
      </button>
      
      <div class="flex items-center gap-3">
        <div class="text-right hidden sm:block">
          <p class="text-sm font-medium text-[var(--text)]">Оператор</p>
          <p class="text-xs text-[var(--text-muted)]">Ситуационный центр</p>
        </div>
        <div class="w-10 h-10 rounded-full bg-[var(--primary)] flex items-center justify-center">
          <span class="text-white font-medium">ОП</span>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Sun, Moon } from 'lucide-vue-next'

const isDark = ref(false)

const toggleTheme = () => {
  isDark.value = !isDark.value
  if (isDark.value) {
    document.documentElement.classList.add('dark')
    localStorage.setItem('theme', 'dark')
  } else {
    document.documentElement.classList.remove('dark')
    localStorage.setItem('theme', 'light')
  }
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme === 'dark') {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }
})
</script>