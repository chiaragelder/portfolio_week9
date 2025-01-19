<template>
  <div class="layout1">
    <ClientOnly>
      <!-- Drawer -->
      <div class="pr-5 z-100">
        <Drawer />
      </div>

      <!-- Main content -->
      <div> 
        <!-- Text content container -->
        <div class="text-container flex flex-col lg:flex-row items-start">
          <!-- Titel aan de linkerkant -->
          <h1 class="text-3xl md:text-3xl lg:text-6xl font-bold text-crimson lg:mb-10 mr-8 max-w-2xl">{{ data.title }}</h1>
          
          <!-- Tags als knoppen tussen titel en body tekst -->
          <div class="tags-buttons mb-8">
            <NuxtLink 
              v-for="(tag, index) in data.tags" 
              :key="index" 
              :to="`/tags/${tag}`" 
              class="tag-button">
              {{ tag }}
            </NuxtLink>
          </div>

          <!-- Rest van de tekst -->
          <div class="text-content">
            <p class="text-lg md:text-2xl lg:text-xl pb-10 text-gray-800 ">{{ data.description }}</p>
            <ContentRenderer :value="data" />
          </div>
        </div>
        
        <!-- Image gallery -->
        <div v-if="data.imagegallery && data.imagegallery.showgallery == true" class="pt-16 pb-24 gallery-container">
          <div class="image-gallery-padding">
            <ImageGallery />
          </div>
        </div>

        <!-- Metadata and divider -->
      </div>

      <div class="text-center mt-40">
        <hr class="footer-line" />
        <div class="mt-4">
          <p class="text-lg text-2xl font-semibold text-crimson">Contact Me!</p>
          <p class="text-sm text-gray-600 text-crimson">chiaragelder@gmail.com</p>
        </div>
      </div>

      <!-- Share Buttons -->
      <ShareButtons />
    
      <!-- SEO metadata -->
      <Title>{{ data.title }}</Title>
      <Meta name="description" :content="data.description" />
      <Meta name="tags" :content="data.tags" />
      <Meta name="keywords" :content="data.tags.join(', ')" />
      <Meta property="og:title" :content="data.title" />
      <Meta property="og:description" :content="data.description" />
      <Meta property="og:image" :content="data.thumbnail" />
      <Meta property="og:url" :content="data.url" />
      <Meta property="og:type" content="article" />
    </ClientOnly>
  </div>
</template>

<style scoped>
/* Basis styling voor het toevoegen van donkere/lichte modus */
:root {
  --text-color-dark: white;
  --text-color-light: black;
  --button-border-dark: #3d3b44;
  --button-border-light: #d3d3d3;
  --button-background-dark: transparent;
  --button-background-light: transparent;
  --button-hover-background-dark: crimson;
  --button-hover-background-light: crimson;
  --button-hover-text-dark: white;
  --button-hover-text-light: white;
}

/* Basis Styling voor de tekstcontainer */
.text-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 16px;
  padding-left: 10%; /* Extra padding links om de tekst meer naar het midden te brengen */
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 100%;
}

/* Flexbox voor titel en tekst naast elkaar op grotere schermen */
.text-container h1 {
  margin-top: 0;
  margin-right: 10px;
  margin-left: 5%; /* Extra ruimte links voor de titel */
  color: crimson;
  font-size: 3rem; /* Grotere titel */
}

/* Tags knoppen - deze zijn flexibel en passen zich aan */
.tags-buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 24px; /* Ruimte tussen tags en body tekst */
  margin-left: 6%; /* Extra ruimte links voor de tags */
}

.tag-button {
  background-color: var(--button-background-dark); /* Geen achtergrondkleur voor dark mode */
  color: var(--text-color-dark); /* Tekstkleur voor dark mode */
  border: 2px solid var(--button-border-dark); /* Randkleur voor dark mode */
  border-color: #3d3b44;
  padding: 5px 10px;
  font-size: 0.875rem;
  cursor: pointer;
  border-radius: 4px;
  text-decoration: none; /* Verwijder onderlijning */
  transition: background-color 0.3s, color 0.3s, border-color 0.3s;
}

/* Knoppen hover-effecten */
.tag-button:hover {
  background-color: var(--button-hover-background-dark); /* Achtergrondkleur bij hover voor dark mode */
  color: var(--button-hover-text-dark); /* Tekstkleur bij hover voor dark mode */
  border-color: var(--button-hover-background-dark); /* Randkleur bij hover voor dark mode */
}

/* Light Mode stijl */
body.light-mode .tag-button {
  background-color: var(--button-background-light); /* Geen achtergrondkleur voor light mode */
  color: var(--text-color-light); /* Tekstkleur voor light mode */
  border: 2px solid var(--button-border-light); /* Randkleur voor light mode */
}

body.light-mode .tag-button:hover {
  background-color: var(--button-hover-background-light); /* Achtergrondkleur bij hover voor light mode */
  color: var(--button-hover-text-light); /* Tekstkleur bij hover voor light mode */
  border-color: var(--button-hover-background-light); /* Randkleur bij hover voor light mode */
}

/* Rest van de tekst container */
.text-content {
  margin-left: 3.7%; /* Extra ruimte links voor de tekst */
  margin-top: 20px;
  max-width: 75ch;  /* Limiteert de lengte van de tekst per regel tot ongeveer 75 tekens */
  line-height: 1.6;
  word-wrap: break-word;  /* Zorgt ervoor dat de tekst goed wordt afgebroken als dat nodig is */
  width: 100%;
}

/* Styling voor de afbeelding en galerij */
.gallery-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.image-gallery-padding {
  width: 100%;
  max-height: 500px;
  overflow: hidden;
}

img {
  width: 100%;
  height: auto;
  object-fit: cover; /* Zorgt ervoor dat de afbeelding zijn aspect ratio behoudt */
}

/* Divider and Last Update */
.metadata-container {
  margin-top: 20px;
  text-align: left;
}

.footer-line {
  border-top: 0.5px  #4b3c3c; /* Dunner dan voorheen */
}

.last-update {
  font-size: 0.75rem; /* Kleinere tekst */
  color: rgba(100, 92, 92, 0.5); /* Grijstint */
  margin-left: 0; /* Links uitgelijnd */
  margin-top: 8px;
}

/* Styling voor beschrijving */
.text-lg {
  font-size: 1.125rem;
}

.text-xl {
  font-size: 1.25rem;
}

.text-2xl {
  font-size: 1.5rem;
}

/* Responsiviteit - Media queries */
@media (max-width: 768px) {
  .text-container {
    padding-left: 5%; /* Minder padding links op kleinere schermen */
  }

  .text-container h1,
  .tags-buttons,
  .text-content {
    margin-left: 2%; /* Minder margin links voor kleinere schermen */
  }
}

@media (max-width: 480px) {
  .text-container h1 {
    font-size: 2rem; /* Kleinere titel op kleine schermen */
  }

  .tag-button {
    font-size: 0.75rem;
  }

  .text-content {
    font-size: 1rem;
  }

  .gallery-container {
    margin-top: 20px;
    max-height: 250px;
  }
}
</style>

<script setup>
defineProps(['data', 'formatDate']);

// Variabele voor het bijhouden van de modus
const isLightMode = ref(false);

// Functie voor het wisselen van modus
function toggleMode() {
  isLightMode.value = !isLightMode.value;
  if (isLightMode.value) {
    document.body.classList.add('light-mode');
    document.body.classList.remove('dark-mode');
  } else {
    document.body.classList.add('dark-mode');
    document.body.classList.remove('light-mode');
  }
}

// Stel de modus in op basis van de systeeminstellingen
if (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches) {
  document.body.classList.add('light-mode');
  document.body.classList.remove('dark-mode');
} else {
  document.body.classList.add('dark-mode');
  document.body.classList.remove('light-mode');
}
</script>
