<script setup lang="ts">
import { ref, computed } from "vue";

const intensity = ref<number>(50);

const bulbStyle = computed(() => {
  // Scale from 0.8 to 1.5 based on intensity 0-100
  const scale = 0.8 + (intensity.value / 100) * 0.7;
  // Dynamic glow based on intensity
  const glow = intensity.value / 4;
  const opacity = 0.3 + (intensity.value / 100) * 0.7;

  return {
    transform: `scale(${scale})`,
    filter: `drop-shadow(0 0 ${glow}px rgba(251, 191, 36, ${opacity}))`,
    color: intensity.value > 0 ? "#fbbf24" : "#94a3b8",
    transition: "transform 0.2s ease, filter 0.2s ease, color 0.3s ease",
  };
});
</script>

<template>
  <div class="dimmer-container">
    <div class="icon-wrapper">
      <svg viewBox="0 0 24 24" class="bulb-icon" :style="bulbStyle">
        <path
          d="M9 21h6v-1H9v1zm3-19C8.14 2 5 5.14 5 9c0 2.38 1.19 4.47 3 5.74V17c0 .55.45 1 1 1h6c.55 0 1-.45 1-1v-2.26c1.81-1.27 3-3.36 3-5.74 0-3.86-3.14-7-7-7z"
          fill="currentColor"
        />
      </svg>
    </div>
    <div class="controls">
      <input
        type="range"
        min="0"
        max="100"
        v-model.number="intensity"
        class="intensity-slider"
      />
      <span class="intensity-value">{{ intensity }}%</span>
    </div>
  </div>
</template>

<style scoped>
.dimmer-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  width: 100%;
}

.icon-wrapper {
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.bulb-icon {
  width: 60px;
  height: 60px;
}

.controls {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.intensity-slider {
  width: 80%;
}

.intensity-value {
  font-family: monospace;
  font-weight: 600;
  color: #38bdf8;
}
</style>
