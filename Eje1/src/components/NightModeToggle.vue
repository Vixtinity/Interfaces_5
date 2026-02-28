<script setup lang="ts">
import { ref } from "vue";

const isNight = ref<boolean>(false);

const toggleNight = () => {
  isNight.value = !isNight.value;
};
</script>

<template>
  <div
    class="toggle-container"
    :class="{ 'is-night': isNight }"
    @click="toggleNight"
  >
    <div class="toggle-track">
      <div class="toggle-thumb">
        <!-- SVG Icon based on mode -->
        <svg v-if="!isNight" viewBox="0 0 24 24" class="icon sun">
          <circle cx="12" cy="12" r="5" fill="currentColor" />
          <path
            d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"
            stroke="currentColor"
            stroke-width="2"
          />
        </svg>
        <svg v-else viewBox="0 0 24 24" class="icon moon">
          <path
            d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"
            fill="currentColor"
          />
        </svg>
      </div>
    </div>
  </div>
</template>

<style scoped>
.toggle-container {
  width: 100px;
  height: 50px;
  background-color: #7dd3fc; /* Sky blue */
  border-radius: 25px;
  padding: 5px;
  cursor: pointer;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: background-color 0.5s ease;
  position: relative;
  overflow: hidden;
}

.toggle-container.is-night {
  background-color: #1e293b; /* Slate dark */
}

.toggle-track {
  width: 100%;
  height: 100%;
  position: relative;
}

.toggle-thumb {
  width: 40px;
  height: 40px;
  background-color: white;
  border-radius: 50%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow:
    0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06);
  transition: transform 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.is-night .toggle-thumb {
  transform: translateX(50px);
}

.icon {
  width: 24px;
  height: 24px;
  color: #fbbf24; /* Sun color */
  transition: color 0.5s ease;
}

.is-night .icon {
  color: #e2e8f0; /* Moon color */
}
</style>
