<template>
  <nav class="navbar merriweather-custom">
    <div class="logo magnetic">Manav.dev</div>
    <ul class="nav-links">
      <li><router-link to="/">Home</router-link></li>
      <li><router-link to="/about">About</router-link></li>
      <li><router-link to="/projects">Projects</router-link></li>
      <li><router-link to="/contact">Contact</router-link></li>
    </ul>
    <!-- <button @click="$emit('toggle-theme')">
      {{ theme === 'dark' ? '☀️' : '🌙' }}
    </button> -->
  </nav>
</template>

<script setup>
// No special logic unless you want to toggle mobile menu
defineProps(['theme'])
</script>

<style lang="scss" scoped>
.navbar {
    box-sizing: border-box;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 80px;
  z-index: 10;

  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
}

.logo{
   font-size: 1.1rem;
    font-weight: 400;
}

  .nav-links {
    font-size: 1.1rem;
    font-weight: 400;
    display: flex;
    gap: 1.5rem;
    list-style: none;

    a {
      color: white;
      text-decoration: none;
      transition: color 0.3s;

      &:hover {
        color: #66ccff;
      }
    }
  }
  :deep(.magnetic) {
  display: inline-block;
  transition: transform 0.3s ease;
  will-change: transform;
  transform: translate(0, 0);
}


</style>
