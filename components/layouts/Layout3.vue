<template>
  <div class="layout2">
    <ClientOnly>
      <div class="relative max-h-screen overflow-hidden z-1">
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
            <h1 class="text-white text-4xl md:text-6xl lg:text-8xl font-bold mb-6 ">{{ data.title }}</h1>
            <h1 v-if="data.subtitle" class="text-white opacity-80 pt-3 text-lg md:text-2xl lg:text-3xl font-bold pb-10">{{ data.subtitle }}</h1>
            <p v-if="data.author" class="text-white opacity-80 text-sm md:text-base lg:text-lg font-bold mb-2">{{ data.author }}</p>
            <!--<p class="text-white text-xs opacity-50 hover:opacity-100">Last update: {{ formatDate(data.date) }}</p>-->
          </div>
        </div>
      </div>

      <div class="absolute top-0 right-0 z-10 pr-5">
        <Drawer /> 
      </div>

      <div class="mx-auto p-4 animate-fade animate-once animate-delay-[500ms]" v-if="imageLoaded">
        <div class="container grid grid-cols-1 md:grid-cols-2 gap-6 mt-6">
          <div>
            <h1 class="text-3xl md:text-4xl lg:text-5xl font-bold mb-4 mijn-tekst">{{ data.title }}</h1>
            <h1 v-if="data.subtitle" class="opacity-80 text-lg md:text-xl lg:text-2xl font-bold pb-6">{{ data.subtitle }}</h1>
            <p class="text-base md:text-lg lg:text-xl pb-6 font-bold">{{ data.description }}</p>
          </div>

          <div>
            <ContentRenderer :value="data" />
            <!-- Tags as buttons (above description) -->
            <div v-if="data.tags" class="tags-buttons mt-4">
              <NuxtLink 
                v-for="(tag, index) in data.tags" 
                :key="index" 
                :to="`/tags/${tag}`" 
                class="tag-button"
              >
                {{ tag }}
              </NuxtLink>
            </div>
          </div>
        </div>

        <div class="max-w-full mx-auto opacity-80 bg-cover px-6 md:px-12 lg:px-16 mt-20">
          <div v-if="data.imagegallery && data.imagegallery.showgallery == true">
            <ImageGallery /> 
          </div>
        </div>

        <div v-if="data.related_page" class="mt-8">
          <RelatedPages :relatedPages="data.related_page" />
        </div>

               <!-- Footer Section -->
      <div class="text-center mt-40">
        <hr />
        <div class="mt-4">
          <p class="text-lg text-2xl font-semibold text-crimson">Contact Me!</p>
          <p class="text-sm text-gray-600 text-crimson">chiaragelder@gmail.com</p>
        </div>
      </div>
      </div>

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
/* Tags buttons styling */
.tags-buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-top: 16px; /* Space above tags buttons */
}

.tag-button {
  background-color: #3d3b44; /* Background color for tags buttons */
  color: white;
  border: none;
  padding: 5px 10px;
  font-size: 0.875rem;
  cursor: pointer;
  border-radius: 4px;
  text-decoration: none; /* Remove underline */
  transition: background-color 0.3s;
}



.tag-button:hover {
  background-color: rgb(173, 18, 49); /* Darker background on hover */
}

.text-blackw{
  color:black
}
</style>
