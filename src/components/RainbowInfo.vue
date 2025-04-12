<script setup lang="ts">
// Componente com informações sobre o arco-íris
</script>

<template>
  <section class="rainbow-info">
    <h2>O que é um Arco-Íris?</h2>
    <div class="info-content">
      <div class="info-text">
        <p>
          O arco-íris é um fenômeno óptico e meteorológico que separa a luz do sol em seu espectro contínuo quando a luz é refletida e refratada pelas gotas de água na atmosfera.
        </p>
        <p>
          Este belo fenômeno ocorre quando a luz solar atravessa gotas de água suspensas no ar, geralmente após uma chuva. A luz branca do sol é composta por várias cores, e quando passa através das gotas de água, cada cor é refratada em um ângulo ligeiramente diferente, criando o espectro colorido que vemos.
        </p>
        <h3>Como se forma?</h3>
        <ol>
          <li>A luz solar (luz branca) entra em uma gota de água suspensa no ar</li>
          <li>A luz é refratada (muda de direção) ao entrar na gota</li>
          <li>A luz é refletida na parte de trás da gota</li>
          <li>A luz é novamente refratada ao sair da gota</li>
          <li>Diferentes comprimentos de onda (cores) são separados</li>
        </ol>
      </div>
      <div class="info-image">
        <img src="../assets/homem-dog-arco-iris.jpeg" alt="Homem com cachorro observando um arco-íris" class="rainbow-photo" />
      </div>
    </div>
  </section>
</template>

<style scoped>
.rainbow-info {
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
  animation: lineExpand 1.2s ease forwards;
}

@keyframes lineExpand {
  from { width: 0; }
  to { width: 100%; }
}

.info-content {
  display: flex;
  gap: 2rem;
  align-items: center;
  position: relative;
  z-index: 2;
}

.info-text {
  flex: 3;
  animation: slideInLeft 0.8s ease forwards;
}

.info-text p {
  margin-bottom: 1.5rem;
  line-height: 1.6;
  color: #444;
}

.info-text h3 {
  margin: 1.5rem 0 1rem;
  color: #333;
  position: relative;
  display: inline-block;
  transition: transform 0.3s ease;
}

.info-text h3::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(to right, #ff7f00, #ffff00);
  transition: width 0.3s ease;
}

.info-text h3:hover::after {
  width: 100%;
}

.info-text h3:hover {
  transform: translateX(3px);
}

.info-text ol {
  padding-left: 1.5rem;
  counter-reset: rainbow-counter;
}

.info-text li {
  margin-bottom: 0.5rem;
  color: #444;
  position: relative;
  padding-left: 0.5rem;
  transition: transform 0.3s ease, color 0.3s ease;
  counter-increment: rainbow-counter;
}

.info-text li::before {
  content: counter(rainbow-counter);
  position: absolute;
  left: -1.5rem;
  width: 1.5rem;
  height: 1.5rem;
  background: linear-gradient(135deg, #ff7f00, #ffff00);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8rem;
  font-weight: bold;
  transition: transform 0.3s ease, background 0.3s ease;
}

.info-text li:hover {
  transform: translateX(5px);
  color: #222;
}

.info-text li:hover::before {
  transform: scale(1.2);
  background: linear-gradient(135deg, #ff0000, #ff7f00);
}

.info-image {
  flex: 2;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: slideInRight 0.8s ease forwards;
}

.rainbow-photo {
  width: 100%;
  max-width: 300px;
  height: auto;
  border-radius: 12px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  animation: float 4s ease-in-out infinite;
}

.rainbow-photo:hover {
  transform: scale(1.03);
  box-shadow: 0 0 25px rgba(0, 0, 0, 0.15);
}

@media (max-width: 768px) {
  .info-content {
    flex-direction: column;
  }
  
  .rainbow-diagram {
    width: 250px;
    height: 250px;
  }
}
</style>