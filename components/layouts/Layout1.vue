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
            <p class="text-lg md:text-2xl lg:text-xl pb-10 text-gray-800">{{ data.description }}</p>
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
        <hr />
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
/* Basis Styling voor de tekstcontainer */
.text-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 16px;
  margin-left: 20px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 100%;
}

/* Flexbox voor titel en tekst naast elkaar op grotere schermen */
.text-container h1 {
  margin-top: 0;
  margin-right: 10px;
  flex: 0 0 auto;
  color: crimson;
  margin-left: 12px;
  font-size: 2rem; /* Zorgt voor betere zichtbaarheid op kleinere schermen */
}

/* Tags knoppen - deze zijn flexibel en passen zich aan */
.tags-buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 24px; /* Ruimte tussen tags en body tekst */
  margin-left: 10px;
}

.tag-button {
  background-color: transparent; /* Geen achtergrondkleur */
  color: rgb(255, 255, 255);
  border: 2px solid #3d3b44; /* Rand rondom de knoppen */
  padding: 5px 10px;
  font-size: 0.875rem;
  cursor: pointer;
  border-radius: 4px;
  text-decoration: none; /* Verwijder onderlijning */
  transition: background-color 0.3s, color 0.3s;
}

.tag-button:hover {
  background-color: crimson; /* Achtergrond wordt rood bij hover */
  color: white;
}

/* Rest van de tekst container */
.text-content {
  padding-left: 0px;
  flex-grow: 1;
  line-height: 1.6;
  margin-top: 20px;
  max-width: 75ch;  /* Limiteert de lengte van de tekst per regel tot ongeveer 75 tekens */
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

.divider {
  width: 100%; /* Volledige breedte */
  border: 0;
  border-top: 1px solid #ccc; /* Lichtgrijze lijn */
  margin: 10px 0;
}

.last-update {
  font-size: 0.75rem; /* Kleinere tekst */
  color: rgba(0, 0, 0, 0.5); /* Grijstint */
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
    padding: 16px;
    margin-left: 0;
  }
  
  .text-container h1 {
    font-size: 1.5rem;
    margin-left: 0;
  }

  .tags-buttons {
    margin-left: 0;
  }

  .text-content {
    margin-top: 10px;
  }

  .gallery-container {
    margin-top: 20px;
    max-height: 300px;
  }
}

@media (max-width: 480px) {
  .text-container h1 {
    font-size: 1.25rem;
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
</script>
