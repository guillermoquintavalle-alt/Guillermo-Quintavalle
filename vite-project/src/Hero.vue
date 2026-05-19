<template>
  <section class="hero">
    <div class="hero-overlay"></div>
    
    <div class="container hero-content">
      <h1>Tu descanso merece <span class="highlight">lo mejor</span></h1>
      <p>Especialistas en la venta de colchones, sommiers de alta densidad y muebles de hogar diseñados para brindarte el máximo confort y estilo.</p>
      <div class="hero-buttons">
        <button type="button" class="cta-button">Ver Catálogo</button>
        <button type="button" @click="isModalOpen = true" class="contact-button">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"></path>
          </svg>
          Contactar
        </button>
      </div>
    </div>

    <div class="modal-overlay" :class="{ 'is-active': isModalOpen }" @click.self="isModalOpen = false">
      <div class="modal-card">
        <button type="button" @click="isModalOpen = false" class="close-btn">&times;</button>
        
        <h3>Nuestros Contactos</h3>
        <p>Elige el medio que prefieras para comunicarte con nosotros:</p>
        
        <div class="modal-links">
          <a href="https://wa.me/543804623869" target="_blank" class="contact-link whatsapp">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"></path>
            </svg>
            WhatsApp: +54 3804 62-3869
          </a>

          <a href="mailto:guillermoquintavalle@gmail.com" class="contact-link gmail">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
              <polyline points="22,6 12,13 2,6"></polyline>
            </svg>
            guillermoquintavalle@gmail.com
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Variable reactiva para controlar el estado visible del modal
const isModalOpen = ref(false)
</script>

<style scoped>
.hero {
  position: relative;
  background-color: var(--text-dark);
  color: var(--bg-white);
  padding: 80px 0;
  text-align: center;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4);
  z-index: 1;
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 700px;
  margin: 0 auto;
}

h1 {
  font-size: 3rem;
  margin-bottom: 20px;
}

.highlight {
  color: var(--primary-orange);
}

p {
  font-size: 1.2rem;
  color: #ccc;
  margin-bottom: 30px;
}

.hero-buttons {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.cta-button {
  background-color: var(--primary-orange);
  color: white;
  border: none;
  padding: 15px 30px;
  font-size: 1.1rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.3s ease;
}

.cta-button:hover {
  background-color: var(--primary-hover);
}

.contact-button {
  background-color: transparent;
  color: white;
  border: 2px solid white;
  padding: 13px 30px;
  font-size: 1.1rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s ease;
}

.contact-button:hover {
  background-color: white;
  color: var(--text-dark);
}

/* --- VENTANA EMERGENTE (MODAL) --- */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999; /* Forzado arriba de todo el layout */
  
  /* Inicialmente oculto mediante CSS */
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

/* Clase que se activa al hacer clic en contactar */
.modal-overlay.is-active {
  opacity: 1;
  pointer-events: auto;
}

.modal-card {
  background-color: var(--bg-white);
  color: var(--text-dark);
  padding: 40px 30px;
  border-radius: 12px;
  max-width: 450px;
  width: 90%;
  position: relative;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  text-align: center;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 20px;
  background: transparent;
  border: none;
  font-size: 2.5rem;
  color: var(--text-gray);
  cursor: pointer;
  line-height: 1;
}

.close-btn:hover {
  color: var(--text-dark);
}

.modal-card h3 {
  font-size: 1.6rem;
  margin-bottom: 10px;
  color: var(--text-dark);
  font-weight: bold;
}

.modal-card p {
  font-size: 0.95rem;
  color: var(--text-gray);
  margin-bottom: 25px;
}

.modal-links {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.contact-link {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  padding: 15px;
  border-radius: 8px;
  text-decoration: none;
  font-weight: bold;
  font-size: 1rem;
  color: white;
  transition: transform 0.2s, filter 0.2s;
  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}

.contact-link:hover {
  transform: translateY(-2px);
  filter: brightness(0.95);
}

.whatsapp {
  background-color: #25D366;
}

.gmail {
  background-color: #EA4335;
}
</style>