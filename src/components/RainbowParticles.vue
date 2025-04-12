<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// Propriedades do componente
interface Props {
  type?: 'rain' | 'sun' | 'both';
  particleCount?: number;
  speed?: number;
}

const props = withDefaults(defineProps<Props>(), {
  type: 'both',
  particleCount: 50,
  speed: 1
});

// Estado para controlar as partículas
const particles = ref<Array<{
  id: number;
  x: number;
  y: number;
  size: number;
  speed: number;
  type: 'rain' | 'sun';
  opacity: number;
  delay: number;
}>>([]);

// Função para inicializar as partículas
const initParticles = () => {
  const newParticles = [];
  const totalParticles = props.particleCount;
  
  for (let i = 0; i < totalParticles; i++) {
    // Determina o tipo de partícula baseado nas props
    let type: 'rain' | 'sun';
    if (props.type === 'both') {
      type = Math.random() > 0.5 ? 'rain' : 'sun';
    } else {
      type = props.type;
    }
    
    // Cria a partícula com propriedades aleatórias
    newParticles.push({
      id: i,
      x: Math.random() * 100, // posição x em porcentagem
      y: Math.random() * 100, // posição y em porcentagem
      size: type === 'rain' ? 2 + Math.random() * 3 : 4 + Math.random() * 6,
      speed: (0.5 + Math.random() * 1.5) * props.speed,
      type,
      opacity: 0.3 + Math.random() * 0.7,
      delay: Math.random() * 5 // atraso para início da animação
    });
  }
  
  particles.value = newParticles;
};

// Variável para armazenar o ID da animação
let animationFrameId: number | null = null;

// Função para animar as partículas
const animateParticles = () => {
  particles.value = particles.value.map(particle => {
    // Lógica de movimento diferente para cada tipo de partícula
    if (particle.type === 'rain') {
      // Gotas de chuva caem para baixo
      particle.y += particle.speed * 0.2;
      // Reinicia a posição quando sai da tela
      if (particle.y > 100) {
        particle.y = -10;
        particle.x = Math.random() * 100;
      }
    } else {
      // Raios de sol movem-se em padrão circular
      const time = Date.now() / 1000;
      const angle = (time * particle.speed * 0.05) + (particle.id * 0.1);
      const radius = 20 + (particle.id % 5) * 5;
      
      particle.x = 50 + Math.cos(angle) * radius;
      particle.y = 50 + Math.sin(angle) * radius;
    }
    
    return particle;
  });
  
  // Continua a animação
  animationFrameId = requestAnimationFrame(animateParticles);
};

// Lifecycle hooks
onMounted(() => {
  initParticles();
  animationFrameId = requestAnimationFrame(animateParticles);
});

onUnmounted(() => {
  // Limpa a animação quando o componente é desmontado
  if (animationFrameId !== null) {
    cancelAnimationFrame(animationFrameId);
  }
});
</script>

<template>
  <div class="rainbow-particles">
    <div 
      v-for="particle in particles" 
      :key="particle.id"
      class="particle"
      :class="[`particle-${particle.type}`]"
      :style="{
        left: `${particle.x}%`,
        top: `${particle.y}%`,
        width: `${particle.size}px`,
        height: particle.type === 'rain' ? `${particle.size * 3}px` : `${particle.size}px`,
        opacity: particle.opacity,
        animationDelay: `${particle.delay}s`
      }"
    ></div>
  </div>
</template>

<style scoped>
.rainbow-particles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
  z-index: 1;
}

.particle {
  position: absolute;
  border-radius: 50%;
}

.particle-rain {
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0.8), rgba(200, 225, 255, 0.4));
  box-shadow: 0 0 5px rgba(255, 255, 255, 0.3);
  border-radius: 40%;
  animation: rainGlow 3s ease-in-out infinite alternate;
}

.particle-sun {
  background: radial-gradient(circle at center, rgba(255, 255, 150, 0.9), rgba(255, 200, 50, 0.6));
  box-shadow: 0 0 8px rgba(255, 200, 50, 0.8);
  animation: sunGlow 2s ease-in-out infinite alternate;
}

@keyframes rainGlow {
  0% { box-shadow: 0 0 3px rgba(255, 255, 255, 0.3); }
  100% { box-shadow: 0 0 7px rgba(200, 225, 255, 0.6); }
}

@keyframes sunGlow {
  0% { box-shadow: 0 0 5px rgba(255, 200, 50, 0.5); }
  100% { box-shadow: 0 0 12px rgba(255, 230, 100, 0.8); }
}
</style>