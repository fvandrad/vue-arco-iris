<script setup lang="ts">
// Componente de galeria de imagens de arco-íris
import { ref } from 'vue';

// Importando as imagens
import arcoIrisMontanhas from '../assets/arco-iris-montanhas.jpeg';
import arcoIrisDuplo from '../assets/arco-iris-duplo.jpeg';
import arcoIrisOceano from '../assets/arco-iris-oceano.jpeg';

interface Image {
  id: number;
  title: string;
  description: string;
  imagePath: string;
}

const images = ref<Image[]>([
  {
    id: 1,
    title: 'Arco-íris sobre montanhas',
    description: 'Um belo arco-íris formado após uma chuva de verão sobre montanhas verdejantes.',
    imagePath: arcoIrisMontanhas
  },
  {
    id: 2,
    title: 'Arco-íris duplo',
    description: 'Um raro fenômeno de arco-íris duplo, onde o segundo arco apresenta as cores em ordem inversa.',
    imagePath: arcoIrisDuplo
  },
  {
    id: 3,
    title: 'Arco-íris sobre o oceano',
    description: 'Um arco-íris majestoso formado sobre o oceano após uma tempestade passageira.',
    imagePath: arcoIrisOceano
  }
]);

const selectedImage = ref<number | null>(null);

function selectImage(id: number) {
  selectedImage.value = selectedImage.value === id ? null : id;
}
</script>

<template>
  <section class="rainbow-gallery">
    <h2>Galeria de Arco-Íris</h2>
    <p class="gallery-intro">Explore belas representações de arco-íris em diferentes cenários.</p>
    
    <div class="gallery-container">
      <div 
        v-for="image in images" 
        :key="image.id"
        class="gallery-item"
        :class="{ selected: selectedImage === image.id }"
        @click="selectImage(image.id)"
      >
        <div class="image-container">
          <img :src="image.imagePath" :alt="image.title" />
        </div>
        <div class="image-info">
          <h3>{{ image.title }}</h3>
          <p v-if="selectedImage === image.id">{{ image.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.rainbow-gallery {
  margin: 3rem 0;
  padding: 2rem;
  background-color: white;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
  overflow: hidden;
  position: relative;
}

.rainbow-gallery::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: linear-gradient(to right, 
    #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3
  );
  z-index: 1;
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

.gallery-intro {
  text-align: center;
  max-width: 800px;
  margin: 2rem auto;
  color: #555;
}

.gallery-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.gallery-item {
  background-color: #fff;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.5s ease;
  transform: translateY(0);
  position: relative;
  animation: scaleIn 0.8s ease forwards;
  opacity: 0;
  cursor: pointer;
}

.gallery-item:nth-child(odd) {
  animation-delay: 200ms;
}

.gallery-item:nth-child(even) {
  animation-delay: 400ms;
}

.gallery-item:hover {
  transform: translateY(-10px) scale(1.03);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
}

.gallery-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  /* background: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.7)); */
  opacity: 0;
  transition: opacity 0.5s ease;
  z-index: 1;
}

.gallery-item:hover::before {
  opacity: 1;
}

.gallery-item.selected {
  grid-column: 1 / -1;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: all 0.5s ease;
  padding: 1.5rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  margin: 1rem 0;
}

.gallery-item.selected .image-container {
  height: 400px;
  width: 80%;
  max-width: 1000px;
  margin: 0 auto;
}

.gallery-item.selected .image-info {
  width: 80%;
  max-width: 1000px;
  margin: 1rem auto;
  text-align: center;
}

.gallery-item.selected .image-info p {
  opacity: 1;
  max-width: 800px;
  margin: 1rem auto;
  font-size: 1.1rem;
}

.image-container {
  height: 200px;
  overflow: hidden;
  background-color: #eee;
  transition: all 0.5s ease;
}

.gallery-item:hover .image-container {
  transform: scale(1.1);
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px 10px 0 0;
  transition: all 0.5s ease;
}

.gallery-item.selected .image-container img {
  object-fit: cover;
  border-radius: 10px;
}

.image-info {
  padding: 1.5rem;
  position: relative;
  z-index: 2;
  transition: transform 0.3s ease;
}

.gallery-item:hover .image-info {
  transform: translateY(-5px);
}

.image-info h3 {
  margin: 0 0 0.5rem 0;
  color: #333;
  position: relative;
  display: inline-block;
  transition: color 0.3s ease;
}

.image-info h3::after {
  content: '';
  position: absolute;
  bottom: -3px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(to right, #ff7f00, #ffff00);
  transition: width 0.3s ease;
}

.gallery-item:hover .image-info h3 {
  color: #ff7f00;
}

.gallery-item:hover .image-info h3::after {
  width: 100%;
}

.image-info p {
  margin: 0;
  color: #555;
  line-height: 1.5;
  transition: opacity 0.3s ease, transform 0.3s ease;
  opacity: 0.8;
}

.gallery-item:hover .image-info p {
  opacity: 1;
  transform: translateY(2px);
}

@media (max-width: 768px) {
  .gallery-container {
    grid-template-columns: 1fr;
  }
}
</style>