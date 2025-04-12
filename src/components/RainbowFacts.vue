<script setup lang="ts">
// Componente com curiosidades sobre o arco-íris
import { ref } from 'vue';

interface Fact {
  id: number;
  title: string;
  description: string;
  icon: string;
}

const facts = ref<Fact[]>([
  {
    id: 1,
    title: 'Arco-íris Duplo',
    description: 'Às vezes, é possível ver dois arco-íris ao mesmo tempo. O segundo arco-íris, mais fraco e mais alto no céu, tem suas cores na ordem inversa do primeiro.',
    icon: '🌈'
  },
  {
    id: 2,
    title: 'Arco-íris Circular',
    description: 'De um avião ou de um ponto muito alto, é possível ver um arco-íris completo formando um círculo, não apenas um arco.',
    icon: '⭕'
  },
  {
    id: 3,
    title: 'Arco-íris Lunar',
    description: 'Um arco-íris lunar ou arco-íris noturno é causado pela luz da lua refletindo nas gotas de água. É muito mais raro e geralmente aparece branco para o olho humano.',
    icon: '🌙'
  },
  {
    id: 4,
    title: 'Arco-íris de Fogo',
    description: 'Um arco-íris de fogo não é realmente um arco-íris, mas um fenômeno óptico raro causado pela luz do sol passando através de cristais de gelo em nuvens cirrus.',
    icon: '🔥'
  },
  {
    id: 5,
    title: 'Sem Fim do Arco-íris',
    description: 'Não é possível chegar ao "fim" de um arco-íris, pois ele é um fenômeno óptico que depende da posição do observador. Se você se mover, o arco-íris também se move.',
    icon: '🏃'
  },
  {
    id: 6,
    title: 'Arco-íris em Outras Culturas',
    description: 'Em muitas culturas, o arco-íris tem significados simbólicos importantes. Na mitologia nórdica, é uma ponte entre a Terra e Asgard; na Irlanda, diz-se que há um pote de ouro no fim do arco-íris.',
    icon: '🌍'
  }
]);

const expandedFact = ref<number | null>(null);

function toggleFact(id: number) {
  expandedFact.value = expandedFact.value === id ? null : id;
}
</script>

<template>
  <section class="rainbow-facts">
    <h2>Curiosidades Sobre Arco-Íris</h2>
    <div class="facts-container">
      <div 
        v-for="fact in facts" 
        :key="fact.id"
        class="fact-card animate-scaleIn"
        :class="{ 'expanded': expandedFact === fact.id }"
        :style="{'animation-delay': (fact.id * 100) + 'ms'}"
        @click="toggleFact(fact.id)"
      >
        <div class="fact-icon">{{ fact.icon }}</div>
        <h3 class="fact-title">{{ fact.title }}</h3>
        <p class="fact-description">{{ fact.description }}</p>
        <!-- <div class="expand-icon">{{ expandedFact === fact.id ? '▲' : '▼' }}</div> -->
      </div>
    </div>
  </section>
</template>

<style scoped>
.rainbow-facts {
  margin: 3rem 0;
  padding: 2rem;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
}

h2 {
  text-align: center;
  margin-bottom: 2rem;
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

.facts-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
  perspective: 1000px; /* Adiciona perspectiva para efeito 3D */
}

.fact-card {
  background-color: white;
  border-radius: 10px;
  padding: 1.5rem;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  transition: transform 0.5s ease, box-shadow 0.5s ease, height 0.5s ease;
  transform-style: preserve-3d;
  position: relative;
  overflow: hidden;
  cursor: pointer;
}

.fact-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.1), rgba(255, 255, 255, 0));
  transform: translateY(-100%);
  transition: transform 0.5s ease;
}

.fact-card:hover {
  transform: translateY(-10px) rotateX(5deg);
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.1);
}

.fact-card:hover::before {
  transform: translateY(0);
}

.fact-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
}

.expand-icon {
  font-size: 1rem;
  color: #777;
  margin-top: 1rem;
  align-self: center;
  transition: transform 0.3s ease;
}

.fact-card.expanded .expand-icon {
  transform: rotate(180deg);
  color: #ff7f00;
}

.fact-card.expanded {
  grid-column: 1 / -1;
  background-color: #f0f8ff;
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
  transition: all 0.5s ease;
  padding: 2rem;
}

.fact-card.expanded .fact-title {
  font-size: 1.6rem;
  margin-bottom: 1.5rem;
  color: #ff7f00;
}

.fact-card.expanded .fact-title::after {
  width: 100%;
  background: linear-gradient(to right, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3);
}

.fact-card.expanded .fact-description {
  font-size: 1.1rem;
  line-height: 1.8;
}

.fact-card.expanded .fact-icon {
  font-size: 3.5rem;
  margin-bottom: 1.5rem;
}

.fact-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  text-align: center;
  transition: transform 0.5s ease;
  animation: float 4s ease-in-out infinite;
}

.fact-card:hover .fact-icon {
  transform: scale(1.2) rotate(10deg);
  animation-duration: 2s;
}

.fact-content {
  flex: 1;
}

.fact-title {
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: #333;
  position: relative;
  padding-bottom: 0.5rem;
  transition: color 0.3s ease;
}

.fact-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(to right, #ff7f00, #ffff00);
  transition: width 0.5s ease;
}

.fact-card:hover .fact-title {
  color: #ff7f00;
}

.fact-card:hover .fact-title::after {
  width: 100%;
}

.fact-description {
  color: #555;
  line-height: 1.6;
  flex: 1;
  transform: translateY(0);
  opacity: 0.9;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.fact-card:hover .fact-description {
  transform: translateY(5px);
  opacity: 1;
}

.expand-icon {
  font-size: 1.5rem;
  color: #777;
  flex-shrink: 0;
}

@media (max-width: 768px) {
  .facts-container {
    grid-template-columns: 1fr;
  }
}
</style>