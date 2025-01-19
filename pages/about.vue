<template>
  <div class="layout1">
    <ClientOnly>
      <!-- Drawer (hamburgermenu) -->
      <div class="pr-5 z-100">
        <Drawer />
      </div>

      <!-- Main content -->
      <div class="content-container">
        <!-- Titel -->
        <h1 class="title">About Me</h1>

        <!-- Container voor afbeelding en tekst -->
        <div class="about-me-container">
          <!-- Afbeelding -->
          <div class="image-container">
            <img src="public/img/IMG_7675.jpeg" alt="Chiara Gelder" class="profile-image" />
          </div>

          <!-- Tekstsectie -->
          <div class="text-section">
            <!-- Chiara Gelder -->
            <div class="text-block">
              <h2 class="text-title">Chiara Gelder</h2>
              <p class="text-content">
                Hi, I am Chiara, a graphic design student at Luca School of Arts. I am 19 years old and currently in my second year of a bachelor’s in Media and Information Design. I’m half Belgian and half Dutch, but I live in Brussels, Belgium.
              </p>
            </div>

            <!-- Mind Studies -->
            <div class="text-block">
              <h2 class="text-title">Mind Studies</h2>
              <p class="text-content">
                My interests mainly lie in the graphic side of design, including book design, creating posters, and making Instagram posts. However, I’m always open to exploring new things!
              </p>
            </div>

            <!-- Other Facts -->
            <div class="text-block">
              <h2 class="text-title">Other Facts</h2>
              <p class="text-content">
                Besides designing, I love dancing, shopping, making notebooks, and especially eating! My favorite food is sushi, which is why I’d love to visit Japan someday—it’s definitely on my travel bucket list. I also really enjoy traveling with friends, family, or my boyfriend.
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
/* Main container for shifting content to the left */
.content-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start; /* Shifts content to the left */
  justify-content: flex-start;
  min-height: 100vh;
  padding-left: 450px; /* Increases space to the left */
  text-align: left; /* Makes sure text is aligned to the left */
}

/* Title styling */
.title {
  font-size: 2.5rem;
  font-weight: bold;
  color: crimson;
  margin-top: 0;
  margin-bottom: 40px;
}

/* Container for image and text */
.about-me-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: flex-start; /* Aligns everything to the left */
  align-items: flex-start; /* Aligns content to the top */
}

/* Image styling */
.image-container {
  flex: 0 0 auto;
  margin-top: 20px;
  margin-right: 60px;
}

.profile-image {
  width: 400px;
  height: 400px;
  border-radius: 15px;
  object-fit: cover;
}

/* Text section styling */
.text-section {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.text-block {
  margin-bottom: 20px;
}

.text-title {
  font-size: 1.5rem;
  font-weight: bold;
  color: crimson;
  margin-bottom: 10px;
}

.text-content {
  font-size: 1rem;
  line-height: 1.6;
  color: #ffffff;
  max-width: 40ch;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

/* Responsiveness for smaller screens */
@media (max-width: 1024px) {
  .about-me-container {
    flex-direction: column;
    align-items: flex-start; /* Ensures everything is aligned to the left */
  }

  .profile-image {
    width: 80%;
    height: auto;
  }

  .text-section {
    text-align: left;
    margin-top: 20px;
  }
}

@media (max-width: 768px) {
  .title {
    font-size: 2rem;
    margin-top: 2rem;
    margin-bottom: 25%;
  }

  .text-title {
    font-size: 1.25rem;
  }

  .text-content {
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .profile-image {
    width: 75%;
  }

  .title {
    font-size: 1.5rem;
  }
}
</style>

<script setup>
defineProps(['tags', 'imageGallery']);
</script>
