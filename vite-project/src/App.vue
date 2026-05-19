<template>
  <div class="app-wrapper">
    <Header />
    <Hero />
    <Location />
    <Catalog />
    
    <footer class="footer">
      <div class="container">
        <p>© 2026 CANON Colchones y Somiers. Todos los derechos reservados.</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import Hero from './components/Hero.vue'
import Location from './components/Location.vue'
import Catalog from './components/Catalog.vue'
</script>

<style scoped>
.app-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
}

.footer {
  margin-top: auto;
  background-color: var(--text-dark);
  color: var(--bg-light);
  text-align: center;
  padding: 20px 0;
  font-size: 0.9rem;
}
</style>