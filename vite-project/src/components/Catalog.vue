<template>
  <section class="catalog-section">
    <div v-if="!selectedProduct" class="catalog-main-view container">
      
      <div class="search-container">
        <div class="search-wrapper">
          <svg class="search-icon" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="11" cy="11" r="8"></circle>
            <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
          </svg>
          <input 
            type="text" 
            v-model="searchQuery" 
            placeholder="¿Qué estás buscando? Ej: Sommier, Almohada..." 
            class="search-input"
            @focus="isDropdownOpen = true"
            @keyup.enter="triggerFirstResult"
          />
          <button v-if="searchQuery" @click="clearSearch" class="clear-search-btn" type="button">&times;</button>
        </div>

        <div v-if="isDropdownOpen && filteredProducts.length > 0 && searchQuery" class="search-dropdown">
          <div 
            v-for="product in filteredProducts" 
            :key="product.id" 
            class="dropdown-item"
            @mousedown.prevent="selectProduct(product)"
          >
            <img :src="product.images[0]" :alt="product.title" class="dropdown-thumb" />
            <div class="dropdown-info">
              <span class="dropdown-title">{{ product.title }}</span>
              <span class="dropdown-price">${{ product.price.toLocaleString('es-AR') }}</span>
            </div>
          </div>
        </div>
      </div>

      <div class="catalog-header">
        <h2 class="section-title">Nuestro Catálogo</h2>
        <div class="carousel-nav">
          <button type="button" @click="scrollSlider('left')" class="nav-btn" aria-label="Anterior">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="15 18 9 12 15 6"></polyline>
            </svg>
          </button>
          <button type="button" @click="scrollSlider('right')" class="nav-btn" aria-label="Siguiente">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
              <polyline points="9 18 15 12 9 6"></polyline>
            </svg>
          </button>
        </div>
      </div>

      <div class="slider-container" ref="slider">
        <div class="product-slider">
          <ProductCard 
            v-for="item in products" 
            :key="item.id"
            :title="item.title"
            :description="item.description"
            :price="item.price"
            :images="item.images"
            class="slider-item"
            @select-product="selectProduct(item)"
          />
        </div>
      </div>
    </div>

    <div v-else class="product-standalone-view container" ref="detailSection">
      <div class="detail-top-bar">
        <button type="button" class="close-detail-square" @click="closeDetail" aria-label="Volver al catálogo">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>
      </div>
      
      <div class="nike-grid">
        <div class="thumbnails-col">
          <div 
            v-for="(img, idx) in selectedProduct.images" 
            :key="idx" 
            class="thumb-wrapper"
            :class="{ 'thumb-active': activeImageIndex === idx }"
            @click="activeImageIndex = idx"
          >
            <img :src="img" alt="Miniatura" />
          </div>
        </div>

        <div class="main-image-col">
          <div class="main-image-wrapper">
            <img :src="selectedProduct.images[activeImageIndex]" :alt="selectedProduct.title" />
          </div>
        </div>

        <div class="product-shop-col">
          <span class="brand-tag">Exclusivo CANON</span>
          <h3 class="detail-title">{{ selectedProduct.title }}</h3>
          <p class="detail-subtitle">Línea de Confort Premium</p>
          
          <div class="price-container">
            <span class="detail-price">${{ selectedProduct.price.toLocaleString('es-AR') }}</span>
            <p class="installments-text">Hasta 6 cuotas de ${{ Math.round(selectedProduct.price / 6).toLocaleString('es-AR') }} sin interés</p>
          </div>

          <div class="sizes-section">
            <div class="sizes-header">
              <span>Seleccionar Medida</span>
              <a href="#" class="size-guide">Guía de medidas</a>
            </div>
            <div class="sizes-grid">
              <button 
                v-for="size in selectedProduct.sizes" 
                :key="size" 
                type="button" 
                class="size-box"
                :class="{ 'size-selected': selectedSize === size }"
                @click="selectedSize = size"
              >
                {{ size }}
              </button>
            </div>
          </div>

          <div class="shop-actions">
            <a :href="'https://wa.me/543804623869?text=Hola!+Me+interesa+el+' + encodeURIComponent(selectedProduct.title) + '+en+medida+' + selectedSize" target="_blank" class="buy-btn whats">
              Encargar por WhatsApp
            </a>
          </div>

          <div class="detail-description-block">
            <h4>Características del producto</h4>
            <p>{{ selectedProduct.description }} Desarrollado con materiales de alta gama, este modelo proporciona una postura óptima durante el descanso, garantizando durabilidad y confort superior en todo momento.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, nextTick, onMounted, onUnmounted } from 'vue';
import ProductCard from './ProductCard.vue';

const slider = ref(null);
const detailSection = ref(null);

// Estados reactivos
const searchQuery = ref('');
const isDropdownOpen = ref(false);
const selectedProduct = ref(null);
const activeImageIndex = ref(0);
const selectedSize = ref('');

// Listado de productos
const products = ref([
  { 
    id: 1, 
    title: 'Sommier Canon Resortes', 
    description: 'Estructura de resortes entrelazados de alta resistencia, ideal para estabilizar la columna y aliviar problemas de espalda.', 
    price: 150000,
    sizes: ['1 1/2 Plaza', '2 Plazas', 'Queen Size', 'King Size'],
    images: [
      'https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=600&auto=format&fit=crop&q=60',
      'https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?w=600&auto=format&fit=crop&q=60'
    ]
  },
  { 
    id: 2, 
    title: 'Colchón Espuma Premium', 
    description: 'Espuma compacta de alta densidad con manta superior de espuma soft y tejido de punto antiácaros totalmente transpirable.', 
    price: 95000,
    sizes: ['1 Plaza', '1 1/2 Plaza', '2 Plazas'],
    images: [
      'https://images.unsplash.com/photo-1540518614846-7eded433c457?w=600&auto=format&fit=crop&q=60',
      'https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=600&auto=format&fit=crop&q=60'
    ]
  },
  { 
    id: 3, 
    title: 'Sommier Canon Sublime', 
    description: 'La máxima expresión del confort. Cuenta con resortes individuales encapsulados (Pocket) que no transmiten el movimiento de un lado a otro.', 
    price: 195000,
    sizes: ['2 Plazas', 'Queen Size', 'King Size'],
    images: [
      'https://images.unsplash.com/photo-1505693416388-ac5ce068fe85?w=600&auto=format&fit=crop&q=60',
      'https://images.unsplash.com/photo-1540518614846-7eded433c457?w=600&auto=format&fit=crop&q=60'
    ]
  },
  { 
    id: 4, 
    title: 'Almohada Inteligente Visco', 
    description: 'Espuma termosensible con memoria que se adapta perfectamente al contorno del cuello y la cabeza. Incluye funda lavable de primera calidad.', 
    price: 18000,
    sizes: ['Estándar (60x40)', 'Cervical Ergonómica'],
    images: [
      'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?w=600&auto=format&fit=crop&q=60',
      'https://images.unsplash.com/photo-1631049307264-da0ec9d70304?w=600&auto=format&fit=crop&q=60'
    ]
  }
]);

const filteredProducts = computed(() => {
  if (!searchQuery.value) return [];
  return products.value.filter(product => 
    product.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

// Activa la vista de producto nueva independiente
const selectProduct = async (product) => {
  selectedProduct.value = product;
  activeImageIndex.value = 0;
  selectedSize.value = product.sizes[0];
  isDropdownOpen.value = false;
  searchQuery.value = ''; // Resetea buscador para cuando se regrese

  await nextTick();
  if (detailSection.value) {
    detailSection.value.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
};

const triggerFirstResult = () => {
  if (filteredProducts.value.length > 0) {
    selectProduct(filteredProducts.value[0]);
  }
};

const clearSearch = () => {
  searchQuery.value = '';
  isDropdownOpen.value = false;
};

const closeDetail = () => {
  selectedProduct.value = null;
};

const closeDropdownOutside = (e) => {
  if (!e.target.closest('.search-container')) {
    isDropdownOpen.value = false;
  }
};

onMounted(() => {
  window.addEventListener('click', closeDropdownOutside);
});

onUnmounted(() => {
  window.removeEventListener('click', closeDropdownOutside);
});

const scrollSlider = (direction) => {
  if (slider.value) {
    const scrollAmount = direction === 'left' ? -300 : 300;
    slider.value.scrollBy({ left: scrollAmount, behavior: 'smooth' });
  }
};
</script>

<style scoped>
.catalog-section {
  position: relative;
  width: 100%;
}

/* --- SOLUCIÓN BARRA DE BÚSQUEDA (Separada de la línea superior blanca) --- */
.search-container {
  position: relative;
  max-width: 550px;
  margin: 40px auto; /* Generoso espacio arriba y abajo */
  z-index: 110;
  padding: 0 15px;
}

.search-wrapper {
  display: flex;
  align-items: center;
  background-color: #f5f5f5;
  border: 2px solid transparent;
  border-radius: 30px;
  padding: 5px 20px;
  transition: all 0.2s ease;
}

.search-wrapper:focus-within {
  background-color: var(--bg-white);
  border-color: var(--text-dark);
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}

.search-icon {
  color: #757575;
  margin-right: 12px;
  flex-shrink: 0;
}

.search-input {
  width: 100%;
  border: none;
  background: none;
  padding: 12px 0;
  font-size: 1rem;
  color: var(--text-dark);
  outline: none;
}

.clear-search-btn {
  background: none;
  border: none;
  font-size: 1.5rem;
  color: #999;
  cursor: pointer;
  padding: 0 5px;
  line-height: 1;
}

/* DESPLEGABLE FLOTANTE */
.search-dropdown {
  position: absolute;
  top: 100%;
  left: 15px;
  right: 15px;
  background-color: var(--bg-white);
  border-radius: 12px;
  margin-top: 8px;
  box-shadow: 0 8px 30px rgba(0,0,0,0.12);
  border: 1px solid #eee;
  max-height: 280px;
  overflow-y: auto;
}

.dropdown-item {
  display: flex;
  align-items: center;
  padding: 12px 20px;
  cursor: pointer;
  transition: background-color 0.15s;
  border-bottom: 1px solid #f9f9f9;
}

.dropdown-item:hover {
  background-color: #f5f5f5;
}

.dropdown-thumb {
  width: 48px;
  height: 48px;
  object-fit: cover;
  border-radius: 6px;
  margin-right: 15px;
  flex-shrink: 0;
}

.dropdown-info {
  display: flex;
  flex-direction: column;
}

.dropdown-title {
  font-weight: 600;
  color: var(--text-dark);
  font-size: 0.95rem;
}

.dropdown-price {
  color: var(--primary-orange);
  font-size: 0.85rem;
  font-weight: 700;
  margin-top: 2px;
}

/* --- MAQUETADO PRINCIPAL DEL CARRUSEL --- */
.catalog-main-view {
  padding: 0 15px;
  animation: fadeIn 0.3s ease-in-out;
}

.catalog-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 25px;
}

.section-title {
  font-size: 2rem;
  color: var(--text-dark);
  margin: 0;
}

.carousel-nav {
  display: flex;
  gap: 10px;
}

.nav-btn {
  background-color: var(--bg-white);
  color: var(--text-dark);
  border: 2px solid #e0e0e0;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-btn:hover {
  background-color: var(--primary-orange);
  color: white;
  border-color: var(--primary-orange);
}

.slider-container {
  width: 100%;
  overflow-x: auto;
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;
  scrollbar-width: none;
  padding-bottom: 20px;
}

.slider-container::-webkit-scrollbar {
  display: none;
}

.product-slider {
  display: flex;
  gap: 20px;
}

.slider-item {
  flex: 0 0 280px;
  scroll-snap-align: start;
}

/* --- 3. VISTA EXCLUSIVA E INDEPENDIENTE DE PRODUCTO --- */
.product-standalone-view {
  padding: 40px 15px;
  animation: fadeIn 0.4s ease-out;
}

.detail-top-bar {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 25px;
}

.close-detail-square {
  background-color: #dc3545;
  color: white;
  border: none;
  width: 44px;
  height: 44px;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(220, 53, 69, 0.2);
  transition: all 0.2s;
}

.close-detail-square:hover {
  background-color: #bd2130;
  transform: scale(1.05);
}

.nike-grid {
  display: grid;
  grid-template-columns: 80px 1fr 420px;
  gap: 40px;
}

.thumbnails-col {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.thumb-wrapper {
  width: 100%;
  height: 80px;
  border-radius: 8px;
  overflow: hidden;
  cursor: pointer;
  border: 2px solid transparent;
  background-color: #f5f5f5;
}

.thumb-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.thumb-active {
  border-color: var(--text-dark);
}

.main-image-col {
  background-color: #f6f6f6;
  border-radius: 16px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 560px;
}

.main-image-wrapper img {
  max-width: 90%;
  max-height: 500px;
  object-fit: contain;
}

.product-shop-col {
  display: flex;
  flex-direction: column;
}

.brand-tag {
  color: var(--primary-orange);
  font-weight: bold;
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.detail-title {
  font-size: 2.4rem;
  font-weight: 800;
  margin: 5px 0 0 0;
  color: var(--text-dark);
}

.detail-subtitle {
  font-size: 1.1rem;
  color: #666;
  margin: 2px 0 25px 0;
}

.price-container {
  margin-bottom: 30px;
}

.detail-price {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text-dark);
}

.installments-text {
  font-size: 0.95rem;
  color: #222;
  margin-top: 4px;
}

.sizes-section {
  margin-bottom: 35px;
}

.sizes-header {
  display: flex;
  justify-content: space-between;
  font-weight: bold;
  margin-bottom: 12px;
}

.size-guide {
  color: #757575;
  text-decoration: underline;
}

.sizes-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 10px;
}

.size-box {
  background-color: white;
  border: 1px solid #e5e5e5;
  padding: 15px;
  border-radius: 8px;
  font-weight: 500;
  cursor: pointer;
  text-align: center;
  transition: all 0.2s;
}

.size-box:hover {
  border-color: var(--text-dark);
}

.size-selected {
  border-color: var(--text-dark);
  background-color: var(--text-dark);
  color: white;
}

.shop-actions {
  margin-bottom: 40px;
}

.buy-btn.whats {
  display: block;
  text-align: center;
  background-color: #25D366;
  color: white;
  padding: 18px;
  border-radius: 30px;
  font-weight: bold;
  text-decoration: none;
  box-shadow: 0 4px 12px rgba(37, 211, 102, 0.2);
  transition: transform 0.2s;
}

.buy-btn.whats:hover {
  transform: scale(1.02);
}

.detail-description-block h4 {
  font-size: 1.1rem;
  margin-bottom: 8px;
}

.detail-description-block p {
  font-size: 0.95rem;
  color: #444;
  line-height: 1.6;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(15px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 950px) {
  .nike-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
  .thumbnails-col {
    flex-direction: row;
    overflow-x: auto;
  }
  .thumb-wrapper {
    width: 75px;
    flex: 0 0 75px;
  }
  .main-image-col {
    height: 360px;
  }
}
</style>