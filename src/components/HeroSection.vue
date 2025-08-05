<!-- src/components/HeroSection.vue -->
<template>
  <section class="hero">
    <div class="hero-content ">
      <h1 ref="title">
        We Design <span class="magnetic">Bold</span><br />
        Custom Unique <br />
        Web/grahpic <br/>
        Experiences
      </h1>
      <!-- <p ref="desc">
        A creative freelance agency crafting modern,<br />
        interactive, and performant websites.
      </p> -->
    </div>
  </section>
</template>
<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

const title = ref(null)
const desc = ref(null)

onMounted(() => {
  gsap.from(title.value, {
    opacity: 0,
    y: 50,
    duration: 1,
    ease: 'power3.out'
  })

  gsap.from(desc.value, {
    opacity: 0,
    y: 100,
    delay: 0.3,
    duration: 1.2,
    ease: 'power4.out'
  })
})
</script>

<style>
.hero {
  padding-top: 10vh;
  min-height: 80vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2rem;
  font-optical-sizing: auto;
  transition: background-color 0.4s, color 0.4s;
}

/* Theme-based styling */
.light .hero {
  background-color: #ffffff;
  color: #121212;
}

.dark .hero {
  background-color: #121212;
  color: #f0f0f0;
}

.hero-content {
  font-family: 'Inter', sans-serif !important;
  text-align: left;
  padding: 0 2rem;
  margin: 0 auto;
}

.hero h1 {
  font-size: 6.5rem;
  font-weight: 700;
  line-height: 1.1;
  margin-bottom: 1.5rem;
  text-transform: uppercase;
}

.hero h1 span {
  font-style: italic;
  transition: color 0.3s ease;
}

/* Themed accent color */
.light .hero h1 span {
  color: #66ccff;
}

.dark .hero h1 span {
  color: #88ddff;
}

.hero p {
  font-size: 1.25rem;
  font-weight: 300;
  line-height: 1.6;
  max-width: 600px;
  margin: 0 auto;
}

:deep(.magnetic) {
  display: inline-block;
  transition: transform 0.3s ease;
  will-change: transform;
  transform: translate(0, 0);
}
</style>
