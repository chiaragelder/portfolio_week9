<template>
  <div class="layout1">
    <ClientOnly>
      <!-- Drawer (hamburgermenu) -->
      <div class="pr-5 z-100">
        <Drawer />
      </div>

      <!-- Main content -->
      <div>
        <!-- Text content container met drie kolommen -->
        <div class="text-container">
          <!-- Titel met uitlijning naar links -->
          <h1 class="text-3xl md:text-3xl lg:text-4xl font-bold text-crimson mb-10">About Me</h1>

          <!-- Drie kolommen -->
          <div class="columns-container">
            <!-- Kolom 1: Chiara Gelder -->
            <div class="column chiara-gelder">
              <h2 class="column-title">Chiara Gelder</h2>
              <p class="column-text text-lg md:text-xl lg:text-lg text-gray-800">
                I am Chiara Gelder, a passionate graphic designer and aspiring web developer.
              </p>
            </div>

            <!-- Kolom 2: Mind Studies -->
            <div class="column mind-studies">
              <h2 class="column-title">Mind Studies</h2>
              <p class="column-text text-lg md:text-xl lg:text-lg text-gray-800">
                I have a strong interest in cognitive science and psychology, which influences my design philosophy.
              </p>
            </div>

            <!-- Kolom 3: Other Facts About Me -->
            <div class="column other-facts">
              <h2 class="column-title">Other Facts</h2>
              <p class="column-text text-lg md:text-xl lg:text-lg text-gray-800">
                I enjoy photography, traveling, and exploring new cultures. I believe in lifelong learning and self-improvement.
              </p>
            </div>
          </div>
        </div>

        <!-- Optional image gallery (if any) -->
        <div v-if="imageGallery && imageGallery.showgallery" class="pt-16 pb-24 gallery-container">
          <div class="image-gallery-padding">
            <ImageGallery />
          </div>
        </div>

        <!-- Metadata and footer -->
        <div class="text-center mt-40">
          <hr class="footer-line" />
          <div class="mt-4">
            <p class="text-lg text-2xl font-semibold text-crimson">Contact Me!</p>
            <p class="text-sm text-gray-600 text-crimson">chiaragelder@gmail.com</p>
          </div>
        </div>
      </div>

      <!-- Share Buttons -->
      <ShareButtons />

      <!-- SEO metadata -->
      <Title>About Me</Title>
      <Meta name="description" content="Learn more about me, a passionate developer." />
      <Meta name="tags" content="developer, Vue.js, Nuxt.js" />
      <Meta name="keywords" content="developer, Vue.js, Nuxt.js" />
      <Meta property="og:title" content="About Me" />
      <Meta property="og:description" content="Learn more about me, a passionate developer." />
      <Meta property="og:image" content="/profile-picture.jpg" />
      <Meta property="og:url" content="/about" />
      <Meta property="og:type" content="article" />
    </ClientOnly>
  </div>
</template>

<style scoped>
/* Styling voor de tekstcontainer */
.text-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 100%;
}

/* Titel styling */
.text-container h1 {
  margin-top: 0;
  color: crimson;
  font-size: 2.5rem; /* Kleinere titel voor 'About Me' */
  text-align: left; /* Zorg ervoor dat de titel links wordt uitgelijnd */
  margin-left: 5%; /* Zorgt voor consistentie met de bodytekst */
  margin-bottom: 40px; /* Verhoogt de afstand tussen de titel en de bodytekst */
}

/* Drie kolommen container */
.columns-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 16px;
  margin-top: 40px;
}

/* Kolommen styling */
.column {
  flex: 1;
  min-width: 250px;
  max-width: 33%;
  padding: 16px;
  box-sizing: border-box;
}

/* Kolomtitels (kleiner) */
.column-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: crimson;
  margin-bottom: 10px;
   margin-left: 16px ;
}

/* Tekst in de kolommen kleiner maken */
.column-text {
  font-size: 1rem; /* Kleinere tekst in de kolommen */
  line-height: 1.6;
}

/* Styling voor de tekst binnen elke kolom */
.text-lg {
  font-size: 1.125rem;
}

.text-xl {
  font-size: 1.25rem;
}

.text-2xl {
  font-size: 1.5rem;
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
  object-fit: cover;
}

/* Divider and Last Update */
.footer-line {
  border-top: 0.5px #ccc;
}

.metadata-container {
  margin-top: 20px;
  text-align: left;
}

/* Responsiviteit - Media queries */
@media (max-width: 768px) {
  .columns-container {
    flex-direction: column; /* Kolommen worden gestapeld op kleinere schermen */
    gap: 20px;
  }

  .column {
    max-width: 100%;
  }

  .text-container h1 {
    font-size: 2rem;
  }

  .column-title {
    font-size: 1.25rem; /* Nog kleinere kolomtitels op kleine schermen */
  }

  .column-text {
    font-size: 0.875rem; /* Kleinere tekst in de kolommen op kleinere schermen */
  }
}
</style>

<script setup>
defineProps(['tags', 'imageGallery']);
</script>
