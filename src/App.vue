<script setup lang="ts">
// Importando componentes
import RainbowHeader from './components/RainbowHeader.vue'
import RainbowInfo from './components/RainbowInfo.vue'
import RainbowColors from './components/RainbowColors.vue'
import RainbowFacts from './components/RainbowFacts.vue'
import RainbowGallery from './components/RainbowGallery.vue'
import RainbowFooter from './components/RainbowFooter.vue'
import RainbowParticles from './components/RainbowParticles.vue'

// Importando arquivo de animações
import './assets/animations.css'
</script>

<template>
  <div class="rainbow-app">
    <RainbowParticles :particle-count="80" type="both" />
    <RainbowHeader class="animate-fadeIn" />
    <main>
      <RainbowInfo class="animate-scaleIn delay-200" />
      <RainbowColors class="animate-slideInLeft delay-400" />
      <RainbowFacts class="animate-slideInRight delay-600" />
      <RainbowGallery class="animate-scaleIn delay-800" />
    </main>
    <RainbowFooter class="animate-fadeIn delay-1000" />
  </div>
</template>

<style>
.rainbow-app {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background: linear-gradient(135deg, #f1f9ff, #e8f4ff, #e0f0ff);
  overflow-x: hidden;
  overflow-y: hidden;

  box-sizing: border-box;
  position: relative;
}

main {
  flex: 1;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

@media (max-width: 768px) {
  main {
    padding: 1rem;
  }
}
</style>
