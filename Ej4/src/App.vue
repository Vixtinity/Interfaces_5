<script setup lang="ts">
import Dashboard from './components/Dashboard.vue';
</script>

<template>
  <div class="app-container">
    <header class="hero">
      <h1>Smart Home Essentials</h1>
      <p>Control total en la palma de tu mano</p>
      <div class="scroll-indicator">Baja para ver la magia ↓</div>
    </header>

    <main>
      <Dashboard />
    </main>
  </div>
</template>

<style>
/* Reset básico y tipografía */
body {
  margin: 0;
  font-family: 'Inter', sans-serif;
  background-color: #f4f7f6;
  color: #333;
}

.app-container {
  display: flex;
  flex-direction: column;
}

/* Forzamos altura para probar el Intersection Observer */
.hero {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%);
  color: white;
}

.scroll-indicator {
  margin-top: 2rem;
  animation: bounce 2s infinite;
}

.spacer {
  height: 50vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #eee;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
  40% {transform: translateY(-10px);}
  60% {transform: translateY(-5px);}
}
</style>