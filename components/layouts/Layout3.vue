<template>
  <div class="layout2">
    <ClientOnly>
      <div class="relative max-h-screen overflow-hidden z-1">
        <!-- Lazy loading applied to NuxtImg -->
        <NuxtImg
          v-if="data.thumbnail"
          :src="data.thumbnail"
          class="w-screen opacity-80 bg-cover mt-6"
          :alt="`Thumbnail for ${data.title}`"
          format="webp"
          loading="lazy"
          @load="imageLoaded = true"
        />
        
        <div v-if="!imageLoaded" class="absolute inset-0 flex items-center justify-center bg-black bg-opacity-75">
          <div class="spinner"></div>
        </div>

        <div
          class="absolute inset-0 flex flex-col items-center justify-center bg-black bg-opacity-50 animate-fade animate-once animate-delay-[500ms]"
          v-if="imageLoaded"
        >
          <div class="p-4 text-center">
            <!-- Responsieve tekst -->
            <h1 class="text-white text-4xl md:text-6xl lg:text-8xl font-bold mb-6 mijn-tekst">{{ data.title }}</h1>
            <h1 v-if="data.subtitle" class="text-white opacity-80 pt-3 text-lg md:text-2xl lg:text-3xl font-bold pb-10">{{ data.subtitle }}</h1>
            <p v-if="data.author" class="text-white opacity-80 text-sm md:text-base lg:text-lg font-bold mb-2">{{ data.author }}</p>
            <p class="text-white text-xs opacity-50 hover:opacity-100">Last update: {{ formatDate(data.date) }}</p>
          </div>
        </div>
      </div>

      <!-- Loading Drawer component (Hamburgermenu) -->
      <div class="absolute top-0 right-0 z-10 pr-5">
        <Drawer /> 
      </div>

      <!-- Main section -->
      <div class="mx-auto p-4 animate-fade animate-once animate-delay-[500ms]" v-if="imageLoaded">
        <div class="container grid grid-cols-1 md:grid-cols-2 gap-6 mt-6">
          <!-- First column -->
          <div>
            <h1 class="text-3xl md:text-4xl lg:text-5xl font-bold mb-4 mijn-tekst">{{ data.title }}</h1>
            <h1 v-if="data.subtitle" class="opacity-80 text-lg md:text-xl lg:text-2xl font-bold pb-6">{{ data.subtitle }}</h1>
            <p class="text-base md:text-lg lg:text-xl pb-6 font-bold">{{ data.description }}</p>
          </div>

          <!-- Second column -->
          <div>
            <ContentRenderer :value="data" />
          </div>
        </div>

        <!-- Image Gallery -->
        <div class="max-w-full mx-auto opacity-80 bg-cover px-6 md:px-12 lg:px-16 mt-8">
          <div v-if="data.imagegallery && data.imagegallery.showgallery == true">
            <ImageGallery /> 
          </div>
        </div>

        <!-- Related pages -->
        <div v-if="data.related_page" class="mt-8">
          <RelatedPages :relatedPages="data.related_page" />
        </div>

        <!-- Link and published date -->
        <div class="text-xs leading-3 mt-8">
          <hr />
          <p class="text-xs opacity-50 hover:opacity-100 pb-2">Last update: {{ formatDate(data.date) }}</p>
          <article v-if="data.tags" class="tags">
            <li v-for="(item, index) in data.tags" :key="index" class="pt-2 text-xs opacity-50 hover:opacity-100">
              <NuxtLink :to="`/tags/${item}`">{{ item }}</NuxtLink>
            </li>
          </article>
        </div>
      </div>

      <!-- Loading the ShareButtons component -->
      <ShareButtons />
    </ClientOnly>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const imageLoaded = ref(false);

defineProps(['data', 'formatDate']);
</script>

<style scoped>
/* Spinner Animation */
.spinner {
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-top: 4px solid #fff;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
}

.title-line-height {
  line-height: 1.6; /* Standaard regelhoogte verhoogd */
}

@media (max-width: 768px) {
  .title-line-height {
    line-height: 1.5; /* Grotere interlinie voor mobiel */
  }
}

@media (min-width: 768px) and (max-width: 1024px) {
  .title-line-height {
    line-height: 1.6; /* Grotere interlinie voor tablets en medium schermen */
  }
}

@media (min-width: 1024px) {
  .title-line-height {
    line-height: 1.7; /* Grotere interlinie voor desktop schermen */
  }
}


/* Keyframe Animatie */
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.mijn-tekst {
  line-height: 1.3 ; /* Stelt de interlinie in op 1.8 keer de lettergrootte */
}

</style>
