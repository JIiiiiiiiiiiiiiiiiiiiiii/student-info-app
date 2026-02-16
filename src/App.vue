<script setup lang="ts">
import HeaderComponent from './components/HeaderComponent.vue'
</script>

<template>
  <div id="app">
    <HeaderComponent />
    <main class="container">
      <router-view />
    </main>
  </div>
</template>

<style scoped>
#app {
  min-height: 100vh;
  background: #0f172a;
}

.container {
  max-width: 1600px;
  margin: 0 auto;
  padding: 2.5rem;
}

@media (max-width: 768px) {
  .container {
    padding: 1.5rem;
  }
}
</style>