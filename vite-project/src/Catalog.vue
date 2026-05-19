<template>
  <section class="catalog container">
    <h2 class="section-title">Nuestro Catálogo</h2>
    <div class="product-grid">
      <ProductCard 
        v-for="item in products" 
        :key="item.id"
        :title="item.title"
        :description="item.description"
        :price="item.price"
      />
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import ProductCard from './ProductCard.vue';

const products = ref([
  { id: 1, title: 'Sommier Canon Resortes', description: 'Alta densidad, ideal para problemas de espalda.', price: 150000 },
  { id: 2, title: 'Colchón Espuma Premium', description: 'Doble plaza, tejido antiácaros transpirable.', price: 95000 },
  { id: 3, title: 'Mesa de Luz Minimalista', description: 'Madera texturizada con detalles en negro.', price: 35000 },
  { id: 4, title: 'Respaldo Capitoné', description: 'Respaldo para cama de 2 plazas, color gris.', price: 42000 },
]);
</script>

<style scoped>
.catalog {
  margin-bottom: 60px;
}

.section-title {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 30px;
  color: var(--text-dark);
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 25px;
}
</style>