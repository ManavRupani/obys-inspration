<template>
  <div :class="theme" class="app-wrapper">
    <NavBar @toggle-theme="toggleTheme" :theme="theme" />
    <HeroSection />
    <ScrollText />
    <CustomCursor />

    <!-- Optional theme toggle if not inside Navbar -->
    <button class="theme-toggle" @click="toggleTheme">
      {{ theme === 'dark' ? '☀️' : '🌙' }}
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import gsap from 'gsap'

import CustomCursor from './components/CustomCursor.vue'
import NavBar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import ScrollText from './components/ScrollText.vue'

const theme = ref('light')
const toggleBtn = ref(null)

onMounted(() => {
  const savedTheme = localStorage.getItem('theme')
  if (savedTheme) theme.value = savedTheme
})

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
  localStorage.setItem('theme', theme.value)

  // Animate button using GSAP
  if (toggleBtn.value) {
    gsap.fromTo(
      toggleBtn.value,
      { rotate: 0 },
      { rotate: 360, duration: 0.5, ease: 'power2.out' }
    )
  }
}
</script>

<style>
.app-wrapper {
  transition: background-color 0.4s ease, color 0.4s ease;
  min-height: 100vh;
}

.light {
  background-color: #ffffff;
  color: #121212;
}

.dark {
  background-color: #121212;
  color: #f0f0f0;
}

.theme-toggle {
  cursor: none;
  position: fixed;
  bottom: 1.5rem;
  right: 1.5rem;
  width: 30px;
  height: 30px;
  z-index: 1000;
  font-size: 1.5rem; /* adjust if using emoji */
  background: transparent;
  border: none;
  /* cursor: pointer; */
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.2s ease;
}

.theme-toggle:hover {
  transform: scale(1.1);
}
</style>
