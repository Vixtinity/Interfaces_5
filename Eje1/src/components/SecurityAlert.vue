<script setup lang="ts">
import { ref } from "vue";

const isAnimating = ref<boolean>(false);

const runInspection = () => {
  if (isAnimating.value) return;

  isAnimating.value = true;

  // Reset after animation completes (roughly 4 seconds)
  setTimeout(() => {
    isAnimating.value = false;
  }, 4000);
};
</script>

<template>
  <div class="security-container">
    <div class="path-preview">
      <!-- A simple SVG path to visualize the drone's trajectory -->
      <svg class="path-visual" viewBox="0 0 300 200">
        <path
          d="M 20 180 Q 150 20 280 180"
          fill="none"
          stroke="rgba(255, 255, 255, 0.1)"
          stroke-dasharray="5,5"
          stroke-width="2"
        />
      </svg>

      <div class="drone-wrapper" :class="{ 'is-inspecting': isAnimating }">
        <svg viewBox="0 0 24 24" class="drone-icon">
          <!-- Drone body -->
          <path
            d="M7 10h10v2H7zM12 6c-1.1 0-2 .9-2 2h4c0-1.1-.9-2-2-2z"
            fill="currentColor"
          />
          <!-- Rotors -->
          <circle cx="5" cy="8" r="2" fill="currentColor" />
          <circle cx="19" cy="8" r="2" fill="currentColor" />
          <circle cx="5" cy="14" r="2" fill="currentColor" />
          <circle cx="19" cy="14" r="2" fill="currentColor" />
        </svg>
      </div>
    </div>
    <button @click="runInspection" :disabled="isAnimating">
      {{ isAnimating ? "Inspeccionando..." : "Test Alarma" }}
    </button>
  </div>
</template>

<style scoped>
.security-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
  width: 100%;
  height: 250px;
  justify-content: flex-end;
  padding-bottom: 1rem;
}

.path-preview {
  position: relative;
  width: 300px;
  height: 200px;
  margin-bottom: -40px;
}

.path-visual {
  width: 100%;
  height: 100%;
}

.drone-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 40px;
  height: 40px;
  color: #38bdf8;
  /* Setting the path */
  offset-path: path("M 20 180 Q 150 20 280 180");
  offset-rotate: auto;
  /* Start position */
  offset-distance: 0%;
  /* Hide when not animating or just show at start? User says test alarm triggers it */
  opacity: 1;
}

.drone-icon {
  width: 100%;
  height: 100%;
  filter: drop-shadow(0 0 8px rgba(56, 189, 248, 0.4));
}

@keyframes drone-path {
  0% {
    offset-distance: 0%;
    transform: scale(1);
  }
  50% {
    offset-distance: 50%;
    transform: scale(1.2);
  }
  100% {
    offset-distance: 100%;
    transform: scale(1);
  }
}

.is-inspecting {
  animation: drone-path 4s ease-in-out forwards;
}
</style>
