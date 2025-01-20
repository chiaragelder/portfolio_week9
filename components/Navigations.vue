<template>
  <div class="opacity-80 animate-fade animate-once animate-delay-[10ms] pt-5">
    <div v-if="navigations.mainmenu.mainavigation_on_off">
      <div class="animate-fade animate-once animate-delay-[150ms]">
        <div v-show="navigations.mainmenu?.mainavigation_on_off">
          <div class="animate-fade animate-once animate-delay-[150ms]">
            <NuxtLink to="/" class="border-none home-button">Home</NuxtLink>

            <!-- Dropdown -->
            <el-collapse v-model="activePanels" accordion class="custom-collapse">
              <el-collapse-item
                title="Works"
                name="1"
                class="custom-collapse-item works-nav"
              >
                <MainNavigation />
              </el-collapse-item>
            </el-collapse>

            <NuxtLink to="/about" class="border-none home-button">About me</NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import MainNavigation from './global/navs/MainNavigation.vue';

// Define the navigations state
const navigations = ref({});
const activePanels = ref([]);

// Use useFetch to load the JSON data from the public folder
const { data, error } = await useFetch('/_data/menus.json');

// Set the data to the navigations ref
if (data.value) {
  navigations.value = data.value;
} else if (error.value) {
  console.error('Error loading navigations:', error.value);
}
</script>

<style scoped>
/* The existing styles for your component remain unchanged */
.opacity-80 {
  opacity: 0.8;
}

::v-deep(.el-collapse-item__content) {
  background-color: transparent !important;
  margin: 0 !important;
  padding: 0 !important;
  border: none !important;
  padding-left: 8px;
}

::v-deep(.el-collapse-item__wrap) {
  background-color: transparent !important;
  border: none !important;
  margin-left: 20px;
  margin-right: 10px;
}

.custom-collapse {
  background-color: transparent !important;
  box-shadow: none !important;
  border: #020027;
}

.custom-collapse-item {
  background-color: transparent !important;
  border: none !important;
  margin: 0 !important;
  padding: 0 !important;
}

::v-deep(.el-collapse-item__header) {
  color: crimson !important;
  background-color: inherit;
  font-size: medium;
  font-weight: 600;
  margin-left: 14px;
  margin-right: 10px;
}

.works-nav .datavisualisatie-title {
  color: crimson !important;
}

.el-collapse {
  background-color: transparent !important;
  box-shadow: none !important;
}

.home-button {
  border: none;
  color: crimson;
  padding: 8px 16px;
  text-decoration: none;
  display: inline-block;
  margin: 0;
}

.home-button:hover {
  background-color: inherit;
  color: crimson;
}

.animate-fade {
  animation: fadeIn 0.5s ease-in-out;
}

.animate-once {
  animation-iteration-count: 1;
}

.animate-delay-[150ms] {
  animation-delay: 150ms;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .home-button {
    padding: 6px 12px;
  }

  .custom-collapse-item {
    padding: 0 !important;
  }
}
</style>