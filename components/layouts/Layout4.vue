<template>
  <div class="layout4">
    <ClientOnly>
    <div class="relative max-h-screen overflow-hidden z-1">
      <!-- Lazy loading applied to NuxtImg -->
      <NuxtImg
        v-if="data.thumbnail"
        :src="data.thumbnail"
        class="w-screen opacity-80 bg-cover"
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
        
      </div>
    </div>

    <!-- Loading Drawer component -->
    <div class="absolute top-0 right-0 z-10 pr-5">
      <Drawer/> 
    </div>

    <!-- Main section -->
    <div class="container mx-auto p-4 animate-fade animate-once animate-delay-[500ms]" v-if="imageLoaded">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
        <!-- First column -->
        <div>
          <h1 class="text-3xl md:text-3xl lg:text-6xl lg:mb-3 font-bold text-crimson ">{{ data.title }}</h1>
          <h1 v-if="data.subtitle" class="opacity-80 text-xl md:text-2xl lg:text-3xl pb-10">{{ data.subtitle }}</h1>
          
          
          <div v-if="data.imagegallery && data.imagegallery.showgallery == true" class="mt-20">
            <ImageGallery/> 
          </div>
        </div>

        <!-- Second column (Text column) -->
        <div class="pl-16 mt-96"> <!-- Added margin-top of 16px -->
          <p class="text-lg md:text-2xl lg:text-xl pb-5 font-bold" style="max-width: 90ch;"> <!-- Increased max-width for longer lines -->
            {{ data.description }}
          </p>
          
          <ContentRenderer :value="data"/>
        </div>
      </div>
      

      <!-- Second row -->
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
      <div v-if="data.related_page">
        <RelatedPages :relatedPages="data.related_page"/>
        
      </div>

      <!-- Link and published date -->
      
    </div>

          <!-- Footer Section -->
      <div class="text-center mt-8">
        <hr />
        <div class="mt-4">
          <p class="text-lg text-2xl font-semibold text-crimson">Contact Me!</p>
          <p class="text-sm text-gray-600 text-crimson">chiaragelder@gmail.com</p>
        </div>
      </div>

    <!-- Loading the ShareButtons component -->
    <ShareButtons/>

    <!-- SEO metadata -->
    <Title>{{ data.title }}</Title>
    <Meta name="description" :content="data.description" />
    <Meta name="tags" :content="data.tags.join(', ')" />
    <Meta name="keywords" :content="data.tags.join(', ')" />
    <Meta property="og:title" :content="data.title" />
    <Meta property="og:description" :content="data.description" />
    <Meta property="og:image" :content="data.thumbnail" />
    <Meta property="og:url" :content="data.url" />
    <Meta property="og:type" content="article" />
  </ClientOnly>
  </div>

</template>

<script setup>
import { ref } from 'vue';
const imageLoaded = ref(false);

defineProps(['data', 'formatDate']);
</script>

<style scoped>
.spinner {
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-top: 4px solid #fff;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
}

/* Styling for the container to push buttons to the right */
.tags-buttons {
  margin-left: 36.3rem;  /* This pushes the whole container to the right */
  margin-right: 0;    /* Optional: To ensure it's at the far right */
  margin-top: 5px;
  margin-bottom: 150px;
}


/* Styling for tag buttons with added large left padding */
.tag-button {
  display: inline-block;
  padding: 0.5rem 1rem;

  margin-top: 0.5rem;
  background-color: #3d3b44;
  color: white;
  text-decoration: none;
  border-radius: 0.375rem;
  font-size: 0.875rem;
  transition: background-color 0.3s;
}

.tag-button:hover {
  background-color: rgb(173, 18, 49);
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.text-crimson{
  color: crimson;
}
</style>
