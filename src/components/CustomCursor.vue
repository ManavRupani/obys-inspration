<template>
  <div class="cursor-outline" ref="cursor"></div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { gsap } from 'gsap'

const cursor = ref(null)

function onMouseMove(e) {
  if (cursor.value) {
    gsap.to(cursor.value, {
      x: e.clientX,
      y: e.clientY,
      duration: 0.3,
      ease: 'power3.out',
    })
  }
  applyMagneticEffect(e) // ✨ pull effect
}

function applyMagneticEffect(e) {
  const magnets = document.querySelectorAll('.magnetic')
  magnets.forEach(el => {
    const rect = el.getBoundingClientRect()
    const relX = e.clientX - rect.left - rect.width / 2
    const relY = e.clientY - rect.top - rect.height / 2
    const distance = Math.sqrt(relX ** 2 + relY ** 2)

    const maxDistance = 120 // range of influence
    if (distance < maxDistance) {
      gsap.to(el, {
        x: relX * 0.4,
        y: relY * 0.4,
        ease: 'power3.out',
        duration: 0.3
      })
    } else {
      gsap.to(el, {
        x: 0,
        y: 0,
        ease: 'power3.out',
        duration: 0.5
      })
    }
  })
}


function updateCursorScaleAndColor(el) {
  if (!cursor.value) return

  if (el.closest('img')) {
  // Bigger radius for image hover
  gsap.to(cursor.value, {
    width: 68,    // ~40 * 1.7 = 68px radius circle
    height: 68,
    duration: 0.3,
  })
} else if (el.closest('.logo')) {
  gsap.to(cursor.value, {
    width: 52,    // ~40 * 1.3 = 52px circle
    height: 52,
    duration: 0.5,
  })
} else if (el.closest('a, button')) {
  gsap.to(cursor.value, {
    width: 60,    // ~40 * 1.5 = 60px circle
    height: 60,
    duration: 0.5,
  })}
  else if (el.closest('span')) {
  gsap.to(cursor.value, {
    width: 120,    // ~40 * 1.5 = 60px circle
    height: 120,
    duration: 0.5,
  })
} else {
  // Default size
  gsap.to(cursor.value, {
    width: 40,
    height: 40,
    duration: 0.5,
  })
}

}

function onMouseOver(e) {
  updateCursorScaleAndColor(e.target)
}

function onMouseOut(e) {
  // On mouse out, revert to default size only if mouse is truly outside any relevant element
  if (!e.relatedTarget) return
  updateCursorScaleAndColor(e.relatedTarget)
}

onMounted(() => {
  window.addEventListener('mousemove', onMouseMove)
  window.addEventListener('mouseover', onMouseOver)
  window.addEventListener('mouseout', onMouseOut)
})

onBeforeUnmount(() => {
  window.removeEventListener('mousemove', onMouseMove)
  window.removeEventListener('mouseover', onMouseOver)
  window.removeEventListener('mouseout', onMouseOut)
})
</script>

<style scoped>
:global(body),
:global(a),
:global(button) {
  cursor: none;
}

.cursor-outline {
  position: fixed;
  top: 0;
  left: 0;
  width: 40px;
  height: 40px;
  border: 0.75px solid rgb(155, 155, 155);
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  mix-blend-mode: difference;
  z-index: 9999;
  transition: background-color 0.3s ease;
  will-change: transform;
}
.magnetic {
  display: inline-block;
  transition: transform 0.3s ease;
  will-change: transform;
  transform: translate(0, 0);
}

</style>
