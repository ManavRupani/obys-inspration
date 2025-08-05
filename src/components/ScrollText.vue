<template>
  <section class="scroll-section" ref="section">
     <!-- <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20"><path d="M10 20A10 10 0 1 0 0 10a10 10 0 0 0 10 10zM8.711 4.3l5.7 5.766L8.7 15.711l-1.4-1.422 4.289-4.242-4.3-4.347z"/></svg> -->
    <div class="image-wrapper">
      
      <img src="https://placehold.co/800x500" alt="Amazing Visual" >
     
    </div>
    <!-- <h2 ref="text">Scroll to Animate Me</h2> -->
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const text = ref(null)

onMounted(() => {
  gsap.from(text.value, {
    scrollTrigger: {
      trigger: text.value,
      start: 'top 95%',
      toggleActions: 'play none none reset'
    },
    y: 50,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  })
})
</script>

<style scoped>
.scroll-section {
  height: 80vh;
  display: flex;
  /* padding-top: 10rem; */
  padding: 10rem;
  align-items: top;
  justify-content: end;
}
</style>
