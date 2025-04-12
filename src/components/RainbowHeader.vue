<script setup lang="ts">
// Componente de cabeçalho para a página do arco-íris
</script>

<template>
  <header class="rainbow-header">
    <div class="rainbow-bar"></div>
    <div class="header-content">
      <h1>O Fascinante Mundo do Arco-Íris</h1>
      <p>"Este é o sinal da aliança que estabeleci entre mim e toda forma de vida sobre a terra", Gênesis 9:17 NTLH</p>
    </div>
  </header>
</template>

<style scoped>
.rainbow-header {
  position: relative;
  padding: 2rem 1rem;
  text-align: center;
  background-color: rgba(255, 255, 255, 0.8);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.rainbow-bar {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 6px;
  background: linear-gradient(to right, 
    #ff0000, /* Vermelho */
    #ff7f00, /* Laranja */
    #ffff00, /* Amarelo */
    #00ff00, /* Verde */
    #0000ff, /* Azul */
    #4b0082, /* Anil */
    #9400d3  /* Violeta */
  );
}

.header-content h1 {
  margin-bottom: 0.5rem;
  font-size: 2.8rem;
  background: linear-gradient(to right, 
    #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3
  );
  background-size: 200% auto;
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transform: translateY(-10px);
  opacity: 0;
  animation: 
    rainbowText 8s linear infinite,
    titleFadeIn 1s ease forwards;
}

@keyframes titleFadeIn {
  from { opacity: 0; transform: translateY(-10px); }
  to { opacity: 1; transform: translateY(0); }
}

.header-content p {
  font-size: 1.3rem;
  color: #555;
  max-width: 600px;
  margin: 0 auto;
  opacity: 0;
  animation: fadeIn 1s ease forwards 0.5s;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  position: relative;
  padding-bottom: 10px;
}

.header-content p::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 2px;
  background: linear-gradient(to right, #ff7f00, #ffff00);
  animation: lineExpand 1.5s ease forwards 1s;
}

@keyframes lineExpand {
  from { width: 0; }
  to { width: 100px; }
}

@keyframes rainbowText {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

@media (max-width: 768px) {
  .header-content h1 {
    font-size: 1.8rem;
  }
  
  .header-content p {
    font-size: 1rem;
  }
}
</style>