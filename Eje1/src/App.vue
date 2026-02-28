<script setup lang="ts">
import NightModeToggle from "./components/NightModeToggle.vue";
import LightDimmer from "./components/LightDimmer.vue";
import SyncStatus from "./components/SyncStatus.vue";
import SecurityAlert from "./components/SecurityAlert.vue";
</script>

<template>
  <main>
    <h1>Smart Home UI Kit</h1>
    <div class="grid">
      <div class="card">
        <h2 class="card-title">Modo Noche</h2>
        <NightModeToggle />
      </div>

      <div class="card">
        <h2 class="card-title">Regulador de Intensidad</h2>
        <LightDimmer />
      </div>

      <div class="card">
        <h2 class="card-title">Sincronización</h2>
        <SyncStatus />
      </div>

      <div class="card">
        <h2 class="card-title">Notificación de Seguridad</h2>
        <SecurityAlert />
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  min-height: 100vh;
  padding: 2rem 0;
}
</style>
