<script setup lang="ts">
// Componente de rodapé para a página do arco-íris
import { ref } from 'vue';

const currentYear = ref(new Date().getFullYear());
</script>

<template>
  <footer class="rainbow-footer">
    <div class="rainbow-bar"></div>
    <div class="footer-content">
      <div class="footer-section">
        <h3>Sobre o Arco-Íris</h3>
        <p>Esta página foi criada para celebrar a beleza e a ciência por trás dos arco-íris, um dos fenômenos naturais mais fascinantes e inspiradores da natureza.</p>
      </div>
      <div class="footer-section">
        <h3>Referências</h3>
        <ul>
          <li><a href="#" target="_blank">Fenômenos Ópticos na Natureza</a></li>
          <li><a href="#" target="_blank">Meteorologia e Arco-Íris</a></li>
          <li><a href="#" target="_blank">Física da Luz e Cores</a></li>
        </ul>
      </div>
      <div class="footer-section">
        <h3>Contato</h3>
        <p>Tem alguma dúvida ou sugestão? Entre em contato conosco:</p>
        <p><a href="mailto:contato@arco-iris.com">contato@arco-iris.com</a></p>
      </div>
    </div>
    <div class="copyright">
      <p>&copy; {{ currentYear }} Mundo do Arco-Íris. Todos os direitos reservados.</p>
    </div>
  </footer>
</template>

<style scoped>
.rainbow-footer {
  position: relative;
  background-color: #333;
  color: #fff;
  padding: 3rem 2rem 1.5rem;
  margin-top: 3rem;
  overflow: hidden;
  box-shadow: 0 -5px 20px rgba(0, 0, 0, 0.1);
}

.rainbow-bar {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 6px;
  background-size: 200% auto;
  animation: rainbowText 8s linear infinite;
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

.footer-content {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  max-width: 1200px;
  margin: 0 auto;
  gap: 2rem;
}

.footer-section {
  flex: 1;
  min-width: 250px;
}

.footer-section h3 {
  color: #fff;
  margin-bottom: 1rem;
  position: relative;
  display: inline-block;
}

.footer-section h3::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 50px;
  height: 2px;
  background: linear-gradient(to right, 
    #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3
  );
}

.footer-section p {
  color: #ccc;
  line-height: 1.6;
}

.footer-section ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-section ul li {
  margin-bottom: 0.5rem;
}

.footer-section a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-section a:hover {
  color: #fff;
  text-decoration: underline;
}

.copyright {
  text-align: center;
  margin-top: 3rem;
  padding-top: 1.5rem;
  border-top: 1px solid #444;
  color: #888;
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
  }
  
  .footer-section {
    margin-bottom: 2rem;
  }
}
</style>