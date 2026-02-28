<script setup lang="ts">
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import FeatureCard from './FeatureCard.vue';
import imagn from '../components/icons/lighting.svg';

// Referencia al contenedor de las tarjetas
const gridRef = ref<HTMLElement | null>(null);

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const cards = entry.target.querySelectorAll('.feature-card');
        
        if (cards.length > 0) {
          gsap.to(cards, {
            duration: 3,
            y: 0,
            rotation: 0,
            opacity: 1,
            ease: "back.out(5)",
            stagger: 1,
            force3D: true
          });
          observer.unobserve(entry.target);
        }
      }
    });
  }, { 
    threshold: 0.2,
    rootMargin: "50px"
  });

  if (gridRef.value) {
    observer.observe(gridRef.value);
  }
});
</script>

<template>
  <section ref="gridRef" class="features-grid">
    <FeatureCard 
      title="Contenedor 1" 
      description="Descripcion del contenedor 1"
      :iconPath="imagn"
    />
    <FeatureCard 
      title="Contenedor 2" 
      description="Descripcion del contenedor 2"
      :iconPath="imagn"
    />
    <FeatureCard 
      title="Contenedor 3" 
      description="Descripcion del contenedor 3"
      :iconPath="imagn"
    />
  </section>
</template>

<style scoped>
.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  padding: 5rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
  min-height: 400px;
}
</style>