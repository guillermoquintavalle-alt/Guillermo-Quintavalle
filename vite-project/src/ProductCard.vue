<template>
  <div class="product-card">
    <div class="img-placeholder">
      <span>Imagen del Producto</span>
    </div>
    <div class="product-details">
      <h4 class="title">{{ title }}</h4>
      <p class="description">{{ description }}</p>
      <div class="price-action">
        <span class="price">${{ price }}</span>
        <button class="buy-btn">Ver más</button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  description: String,
  price: Number
})
</script>

<style scoped>
.product-card {
  background-color: var(--bg-white);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.2s, box-shadow 0.2s;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

.img-placeholder {
  background-color: #e9ecef;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-gray);
  font-size: 0.9rem;
}

.product-details {
  padding: 20px;
}

.title {
  font-size: 1.1rem;
  margin-bottom: 8px;
  color: var(--text-dark);
}

.description {
  font-size: 0.9rem;
  color: var(--text-gray);
  margin-bottom: 15px;
  height: 40px;
}

.price-action {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.price {
  font-size: 1.2rem;
  font-weight: bold;
  color: var(--canon-green);
}

.buy-btn {
  background-color: transparent;
  border: 1px solid var(--primary-orange);
  color: var(--primary-orange);
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s;
}

.buy-btn:hover {
  background-color: var(--primary-orange);
  color: white;
}
</style>