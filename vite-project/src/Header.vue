<template>
  <header class="header">
    <div class="container header-content">
      <div class="logo">
        <span class="logo-text">CANON</span>
        <span class="logo-sub">Colchones & Somiers</span>
      </div>
      
      <div class="search-bar">
        <input type="text" placeholder="Buscar productos..." />
        <button class="search-btn">
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="11" cy="11" r="8"></circle>
            <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
          </svg>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  background-color: var(--bg-white);
  border-bottom: 2px solid var(--border-color);
  padding: 15px 0;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  flex-direction: column;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 900;
  color: var(--canon-green);
  letter-spacing: 1px;
}

.logo-sub {
  font-size: 0.8rem;
  color: var(--text-gray);
}

.search-bar {
  display: flex;
  align-items: center;
  background-color: var(--bg-light);
  border: 1px solid var(--border-color);
  border-radius: 25px;
  overflow: hidden;
  padding: 2px 15px;
}

.search-bar input {
  border: none;
  background: transparent;
  padding: 8px;
  outline: none;
  width: 200px;
}

.search-btn {
  background: transparent;
  border: none;
  color: var(--primary-orange);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>