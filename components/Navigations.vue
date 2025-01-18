<template>
  <div class="opacity-80 animate-fade animate-once animate-delay-[10ms] pt-5">

    <div v-if="navigations.mainmenu.mainavigation_on_off">
      <div class="animate-fade animate-once animate-delay-[150ms]">
        <div v-show="navigations.mainmenu?.mainavigation_on_off">
          <div class="animate-fade animate-once animate-delay-[150ms]">
            <NuxtLink to="/" class="border-none home-button">Home</NuxtLink>

            <!-- Dropdown -->
            <el-collapse v-model="activePanels" accordion class="custom-collapse">
              <el-collapse-item title="Works" name="1" class="custom-collapse-item works-nav" >
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
import { text } from 'stream/consumers';

const navigations = ref({});
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
/* Basis Styling voor de tekstcontainer */
.opacity-80 {
  opacity: 0.8;
}

/* Verwijder de achtergrondkleur, padding/margin van de dropdown en nav-items */
.custom-collapse {
  background-color: transparent !important; /* Verwijder de achtergrondkleur van de collapse */
  box-shadow: none !important; /* Verwijder schaduwen van de collapse */
  border: #020027;
}

.custom-collapse-item {
  background-color: transparent !important;  /* Verwijder de achtergrondkleur van de collapse items */
  border: none !important;                   /* Verwijder de rand */
  margin: 0 !important;                      /* Verwijder marges */
  padding: 0 !important;                     /* Verwijder padding */
}

/* Zorg ervoor dat de titel van de dropdown naar crimson rood gaat */
.el-collapse-item__header {
  color: crimson !important;  /* Verander de kleur van de titel naar crimson */
  
}

/* Als je specifieke items zoals "Datavisualisatie" wilt stylen, voeg je de class toe */
.works-nav .datavisualisatie-title {
  color: crimson !important;  /* Verander de kleur naar crimson voor Datavisualisatie titel */
}

.el-collapse {
  background-color: transparent !important;  /* Zorg ervoor dat de collapse-container geen achtergrond heeft */
  box-shadow: none !important;  /* Verwijder de schaduw van de collapse */
}

/* Styling voor de dropdown-links om marges en randen te verwijderen */
.home-button {
  border: none; /* Verwijder de rand rondom de buttons */
  color: crimson; /* Zorg ervoor dat de kleur van de links goed overgenomen wordt */
  padding: 8px 16px;  /* Voeg wat padding toe als dat nodig is */
  text-decoration: none; /* Verwijder onderlijning */
  display: inline-block; /* Zorg ervoor dat de links goed in lijn blijven */
  margin: 0; /* Verwijder marges van de links */
}

/* Styling voor hover-effecten op de links */
.home-button:hover {
  background-color: #020027;  /* Toevoegen van een lichte achtergrondkleur op hover */
  color: crimson;  /* Verander de kleur van de tekst */
  
}

/* Aanpassingen voor de fade-in animaties */
.animate-fade {
  animation: fadeIn 0.5s ease-in-out;
}

.animate-once {
  animation-iteration-count: 1;
}

.animate-delay-[150ms] {
  animation-delay: 150ms;
}

/* Animatie definitie */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Responsieve aanpassingen (indien nodig) */
@media (max-width: 768px) {
  .home-button {
    padding: 6px 12px; /* Kleinere padding voor mobiele weergave */
  }

  .custom-collapse-item {
    padding: 0 !important; /* Zorg ervoor dat de dropdown geen extra padding heeft */
  }
}
</style>
