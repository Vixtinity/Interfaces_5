<script setup lang="ts">
import { ref } from "vue";

const isSyncing = ref<boolean>(false);

const startSync = () => {
  if (isSyncing.value) return;

  isSyncing.value = true;

  // Stop after 3 seconds as required
  setTimeout(() => {
    isSyncing.value = false;
  }, 3000);
};
</script>

<template>
  <div class="sync-container">
    <div class="icon-wrapper" :class="{ 'is-syncing': isSyncing }">
      <svg viewBox="0 0 24 24" class="sync-icon">
        <path
          d="M12 4V1L8 5l4 4V6c3.31 0 6 2.69 6 6 0 1.01-.25 1.97-.7 2.8l1.46 1.46C19.54 15.03 20 13.57 20 12c0-4.42-3.58-8-8-8zm0 14c-3.31 0-6-2.69-6-6 0-1.01.25-1.97.7-2.8L5.24 7.74C4.46 8.97 4 10.43 4 12c0 4.42 3.58 8 8 8v3l4-4-4-4v3z"
          fill="currentColor"
        />
      </svg>
    </div>
    <button @click="startSync" :disabled="isSyncing" class="sync-button">
      {{ isSyncing ? "Sincronizando..." : "Sincronizar" }}
    </button>
  </div>
</template>

<style scoped>
.sync-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.5rem;
}

.icon-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60px;
  height: 60px;
  color: #38bdf8;
}

.sync-icon {
  width: 40px;
  height: 40px;
}

/* Keyframes for rotation */
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

/* Apply animation only when syncing */
.is-syncing .sync-icon {
  animation: rotate 1s linear infinite;
}

.sync-button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  background: #334155;
}
</style>
