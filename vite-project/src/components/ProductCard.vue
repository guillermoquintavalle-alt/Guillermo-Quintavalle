<template>
  <div class="product-card">
    <div class="card-image-wrapper">
      <img :src="images[0]" :alt="title" class="card-img" />
    </div>
    <div class="card-content">
      <h3 class="card-title">{{ title }}</h3>
      <p class="card-description">{{ truncateText(description, 60) }}</p>
      <div class="card-footer">
        <span class="card-price">${{ price.toLocaleString('es-AR') }}</span>
        <button type="button" class="view-more-btn" @click="$emit('select-product')">
          Ver más
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  description: String,
  price: Number,
  images: Array
});

defineEmits(['select-product']);

const truncateText = (text, limit) => {
  if (text.length <= limit) return text;
  return text.substring(0, limit) + '...';
};
</script>

<style scoped>
.product-card {
  background-color: var(--bg-white);
  border-radius: 12px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  height: 100%;
  transition: transform 0.2s ease;
}

.product-card:hover {
  transform: translateY(-4px);
}

.card-image-wrapper {
  width: 100%;
  height: 180px;
  overflow: hidden;
  background-color: #f0f0f0;
}

.card-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-content {
  padding: 15px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.card-title {
  font-size: 1.1rem;
  color: var(--text-dark);
  margin: 0 0 8px 0;
  font-weight: 700;
}

.card-description {
  font-size: 0.85rem;
  color: #666;
  margin: 0 0 15px 0;
  line-height: 1.4;
  flex-grow: 1;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.card-price {
  font-weight: 700;
  color: var(--text-dark);
  font-size: 1.1rem;
}

.view-more-btn {
  background-color: var(--text-dark);
  color: white;
  border: none;
  padding: 8px 14px;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s;
}

.view-more-btn:hover {
  background-color: var(--primary-orange);
}
</style>