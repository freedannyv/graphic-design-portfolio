<template>
  <section class="flex flex-col items-center justify-center min-h-screen text-center px-6 bg-bg-primary transition-colors duration-300">
    <button 
      @click="toggleTheme" 
      class="absolute top-6 right-6 p-3 rounded-full bg-bg-secondary text-text-primary hover:bg-accent hover:text-white transition-colors"
      :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
    >
      <svg v-if="isDark" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
      </svg>
      <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
      </svg>
    </button>
    <h1 class="text-5xl font-bold mb-4 text-text-primary">Welcome to My Portfolio</h1>
    <p class="text-xl text-text-secondary mb-8">This is the homepage of my Nuxt portfolio website.</p>
    <a href="#" class="px-6 py-3 bg-accent text-white font-semibold rounded-lg hover:bg-accent-hover transition-colors">
      View My Work
    </a>
  </section>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

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
  if (savedTheme === 'dark' || (!savedTheme && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    isDark.value = true
    document.documentElement.classList.add('dark')
  }
})
</script>
