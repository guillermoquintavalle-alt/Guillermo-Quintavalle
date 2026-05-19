<template>
  <section class="location-section container">
    <div class="location-card">
      <div class="location-header">
        <div class="icon-wrapper">
          <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
            <circle cx="12" cy="10" r="3"></circle>
          </svg>
        </div>
        <div class="location-info">
          <h3>Visita nuestro Showroom</h3>
          <p>Encuentra el colchón perfecto probándolo tú mismo en nuestra sucursal.</p>
        </div>
        
        <div class="contact-action">
          <a href="https://wa.me/543804623869" target="_blank" class="whatsapp-btn">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 11.5a8.38 8.38 0 0 1-.9 3.8 8.5 8.5 0 0 1-7.6 4.7 8.38 8.38 0 0 1-3.8-.9L3 21l1.9-5.7a8.38 8.38 0 0 1-.9-3.8 8.5 8.5 0 0 1 4.7-7.6 8.38 8.38 0 0 1 3.8-.9h.5a8.48 8.48 0 0 1 8 8v.5z"></path>
            </svg>
            Consultar por WhatsApp
          </a>
        </div>
      </div>

      <div class="map-container">
        <iframe 
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2818.2131762994086!2d-66.85534966695414!3d-29.439280065509788!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x9427db88743962a1%3A0x77f26ee2aa7e0a7e!2sConfort%20La%20Rioja!5e0!3m2!1ses-419!2sar!4v1779158039591!5m2!1ses-419!2sar" 
          style="border:0;" 
          allowfullscreen="" 
          loading="lazy" 
          referrerpolicy="no-referrer-when-downgrade">
        </iframe>
      </div>
    </div>
  </section>
</template>

<style scoped>
.location-section {
  margin: 40px auto;
}

.location-card {
  background-color: var(--bg-white);
  border-top: 5px solid var(--canon-green);
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.05);
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.location-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
}

.icon-wrapper {
  color: var(--primary-orange);
  display: flex;
  align-items: center;
}

.location-info {
  flex: 1;
  min-width: 250px;
}

h3 {
  font-size: 1.4rem;
  margin-bottom: 5px;
  color: var(--text-dark);
}

p {
  color: var(--text-gray);
}

/* --- ESTILOS DEL MAPA RESPONSIVO --- */
.map-container {
  width: 100%;
  height: 400px; /* Altura fija ideal para web */
  border-radius: 8px;
  overflow: hidden;
  box-shadow: inset 0 0 10px rgba(0,0,0,0.1);
  border: 1px solid var(--border-color);
}

.map-container iframe {
  width: 100%;
  height: 100%;
}

/* --- BOTÓN DE WHATSAPP --- */
.whatsapp-btn {
  background-color: #25D366;
  color: white;
  text-decoration: none;
  padding: 12px 22px;
  border-radius: 25px;
  font-weight: bold;
  display: flex;
  align-items: center;
  gap: 10px;
  box-shadow: 0 4px 12px rgba(37, 211, 102, 0.2);
  transition: transform 0.2s, background-color 0.2s;
}

.whatsapp-btn:hover {
  background-color: #20ba56;
  transform: scale(1.03);
}

/* Ajustes para pantallas chicas/celulares */
@media (max-width: 600px) {
  .location-header {
    flex-direction: column;
    text-align: center;
  }
  .contact-action {
    width: 100%;
    display: flex;
    justify-content: center;
  }
  .map-container {
    height: 300px; /* Reducimos un poco la altura en celulares */
  }
}
</style>