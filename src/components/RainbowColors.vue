<script setup lang="ts">
// Componente que exibe as cores do arco-íris e seus significados
import { ref } from 'vue';

interface RainbowColor {
  name: string;
  hexCode: string;
  description: string;
  wavelength: string;
}

const colors = ref<RainbowColor[]>([
  {
    name: 'Vermelho',
    hexCode: '#FF0000',
    description: 'A primeira cor do arco-íris, simboliza energia, paixão e vitalidade.',
    wavelength: '620-750 nm'
  },
  {
    name: 'Laranja',
    hexCode: '#FF7F00',
    description: 'Representa entusiasmo, criatividade e alegria.',
    wavelength: '590-620 nm'
  },
  {
    name: 'Amarelo',
    hexCode: '#FFFF00',
    description: 'Simboliza otimismo, clareza e felicidade.',
    wavelength: '570-590 nm'
  },
  {
    name: 'Verde',
    hexCode: '#00FF00',
    description: 'Associado à natureza, crescimento, harmonia e renovação.',
    wavelength: '495-570 nm'
  },
  {
    name: 'Azul',
    hexCode: '#0000FF',
    description: 'Representa tranquilidade, confiança e serenidade.',
    wavelength: '450-495 nm'
  },
  {
    name: 'Anil',
    hexCode: '#4B0082',
    description: 'Simboliza intuição, percepção e profundidade.',
    wavelength: '420-450 nm'
  },
  {
    name: 'Violeta',
    hexCode: '#9400D3',
    description: 'Associado à espiritualidade, mistério e transformação.',
    wavelength: '380-420 nm'
  }
]);

const activeColor = ref<number | null>(null);

function setActiveColor(index: number) {
  activeColor.value = activeColor.value === index ? null : index;
}
</script>

<template>
  <section class="rainbow-colors">
    <h2>As Cores do Arco-Íris</h2>
    <p class="intro-text">
      O arco-íris tradicional é composto por sete cores principais, cada uma com seu próprio comprimento de onda e significado cultural.
    </p>
    
    <div class="colors-container">
      <div 
        class="color-card animate-scaleIn" 
        v-for="(color, index) in colors" 
        :key="color.name"
        :class="{ active: activeColor === index }"
        @click="setActiveColor(index)"
        :style="{ '--color': color.hexCode, 'animation-delay': index * 100 + 'ms' }"
      >
        <div class="color-sample" :style="{ backgroundColor: color.hexCode }"></div>
        <h3 class="color-name">{{ color.name }}</h3>
        <div class="color-details" v-if="activeColor === index">
          <p class="color-description">{{ color.description }}</p>
          <span class="color-wavelength">{{ color.wavelength }}</span>
        </div>
      </div>
    </div>
    
    <div class="rainbow-spectrum">
      <div class="spectrum-bar"></div>
      <div class="spectrum-labels">
        <span>Comprimentos de onda mais longos</span>
        <span>Comprimentos de onda mais curtos</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.rainbow-colors {
  margin: 3rem 0;
  padding: 2rem;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

h2 {
  text-align: center;
  margin-bottom: 1rem;
  color: #333;
  position: relative;
  display: inline-block;
  left: 50%;
  transform: translateX(-50%);
}

h2::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 0;
  width: 100%;
  height: 3px;
  background: linear-gradient(to right, 
    #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3
  );
  border-radius: 3px;
}

.intro-text {
  text-align: center;
  max-width: 800px;
  margin: 2rem auto;
  color: #555;
}

.colors-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1.5rem;
  margin: 2rem 0;
}

.color-card {
  background-color: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
  overflow: hidden;
  z-index: 1;
}

.color-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
}

.color-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: var(--color);
  z-index: 2;
  transition: height 0.3s ease;
}

.color-card:hover::before {
  height: 10px;
}

.color-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
}

.color-card.active {
  width: 100%;
  max-width: 600px;
}

.color-sample {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  margin-bottom: 1rem;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  animation: pulse 3s ease-in-out infinite;
}

.color-card:hover .color-sample {
  transform: scale(1.1);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  animation: pulse 1.5s ease-in-out infinite;
}

/* .color-card.active .color-sample {
  height: 120px;
} */

.color-info {
  padding: 1rem;
}

.color-name {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  transition: color 0.3s ease, transform 0.3s ease;
  position: relative;
}

.color-card:hover .color-name {
  transform: scale(1.05);
  color: var(--color);
}

.color-name::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 2px;
  background: var(--color);
  transition: width 0.3s ease;
}

.color-card:hover .color-name::after {
  width: 100%;
}

.color-description {
  font-size: 0.9rem;
  color: #666;
  margin-bottom: 1rem;
  transition: opacity 0.3s ease;
  opacity: 0.8;
}

.color-card:hover .color-description {
  opacity: 1;
}

.color-wavelength {
  font-size: 0.8rem;
  color: #888;
  background-color: #f5f5f5;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease;
}

.color-card:hover .color-wavelength {
  background-color: var(--color);
  color: white;
  transform: scale(1.05);
}

.rainbow-spectrum {
  margin-top: 3rem;
  text-align: center;
}

.spectrum-bar {
  height: 20px;
  background: linear-gradient(to right, 
    #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3
  );
  border-radius: 10px;
  margin-bottom: 0.5rem;
}

.spectrum-labels {
  display: flex;
  justify-content: space-between;
  font-size: 0.9rem;
  color: #777;
}

@media (max-width: 768px) {
  .color-card {
    width: 100%;
  }
  
  .color-card.active {
    max-width: 100%;
  }
}
</style>