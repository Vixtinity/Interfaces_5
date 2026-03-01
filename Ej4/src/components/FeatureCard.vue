<script setup lang="ts">
import { ref } from 'vue';

interface Props {
  title: string;
  description: string;
  iconPath: string;
}

defineProps<Props>();

// Exponemos el elemento para que el padre pueda usarlo en la Ref
const cardElement = ref<HTMLElement | null>(null);
defineExpose({ cardElement });
</script>

<template>
  <div ref="cardElement" class="feature-card">
    <img :src="iconPath" :alt="title" class="icon" />
    <h3>{{ title }}</h3>
    <p>{{ description }}</p>
  </div>
</template>

<style scoped>
.feature-card {
  /* ... tu código actual ... */
  opacity: 0; 
  transform: translateY(50px) rotate(5deg); 
  padding: 2rem;
  border-radius: 12px;
  background: white;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
  text-align: center;
  transition: none; 
  width: 250px;
  /* Añadimos flex para centrar contenido */
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* ESTO ES LO QUE NECESITAS */
.icon {
  width: 60px;   /* Ajusta a tu gusto */
  height: 60px;  /* Ajusta a tu gusto */
  object-fit: contain;
  margin-bottom: 1rem;
}
</style>