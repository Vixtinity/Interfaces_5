<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

const canvasRef = ref<HTMLCanvasElement | null>(null);
let animationFrameId: number;
let phase = 0; 

const draw = (ctx: CanvasRenderingContext2D, width: number, height: number) => {
  ctx.fillStyle = '#000';
  ctx.fillRect(0, 0, width, height);
  
  ctx.beginPath();
  ctx.lineWidth = 2;
  ctx.strokeStyle = '#ff8000';

  const centerY = height / 2;
  const amplitude = 12;
  const frequency = 0.10;

  for (let x = 0; x < width; x++) {
    const y = centerY + Math.sin(x * frequency + phase) * amplitude;
    x === 0 ? ctx.moveTo(x, y) : ctx.lineTo(x, y);
  }

  ctx.stroke();
  phase += 0.1; // Velocidad del movimiento
};

onMounted(() => {
  const canvas = canvasRef.value;
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  if (!ctx) return;

  canvas.width = 600;
  canvas.height = 300;

  const animate = () => {
    draw(ctx, canvas.width, canvas.height);
    animationFrameId = requestAnimationFrame(animate);
  };
  animate();
});

onUnmounted(() => cancelAnimationFrame(animationFrameId));
</script>

<template>
  <div class="container">
    <canvas ref="canvasRef"></canvas>
  </div>
</template>

<style scoped>
.container {
  text-align: center;
  font-family: sans-serif;
}

canvas {
  display: block;
  margin-left: 1000px auto;
  background: #000;
  border: 1px solid #ccc;
}
</style>