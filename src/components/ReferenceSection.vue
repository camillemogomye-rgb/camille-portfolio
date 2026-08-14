<template>
  <section id="portfolio" class="reference-section">
    <div class="reference-header">
      <p class="sous-titre">Des projets réalisés avec succès</p>
      <span class="horizontal-lign"></span>
      <h2>MES RÉALISATIONS</h2>
    </div>

    <!-- Conteneur global du carrousel avec contrôle et drag -->
    <div class="slider-wrapper">
      <!-- Bouton Flèche Gauche (Translucide) -->
      <button
        class="nav-btn btn-left"
        @click="scrollManual('left')"
        aria-label="Précédent"
      >
        &#10094;
      </button>

      <!-- Zone de Défilement / Drag -->
      <div
        class="slider-container"
        ref="sliderRef"
        @mouseenter="pauseAutoScroll"
        @mouseleave="resumeAutoScrollWithDelay"
        @mousedown="startDrag"
        @mouseup="stopDragWithDelay"
        @mousemove="onDrag"
      >
        <div
          class="slider-track"
          :class="{ 'is-paused': isPaused, 'is-dragging': isDragging }"
          :style="trackStyle"
        >
          <!-- Quadruplication dynamique pour flux continu -->
          <div
            class="project-card"
            v-for="(project, index) in seamlessProjects"
            :key="index"
          >
            <div class="mockup-wrapper">
              <img
                :src="getImageUrl(project.mockup)"
                :alt="project.titre"
                draggable="false"
              />
            </div>

            <a
              :href="project.url"
              target="_blank"
              rel="noopener noreferrer"
              class="project-title-link"
            >
              <h3 class="project-title">{{ project.titre }}</h3>
            </a>

            <div class="project-skills">
              <span
                class="skill"
                v-for="(skill, sIndex) in project.skills"
                :key="sIndex"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </div>

      <!-- Bouton Flèche Droite (Translucide) -->
      <button
        class="nav-btn btn-right"
        @click="scrollManual('right')"
        aria-label="Suivant"
      >
        &#10095;
      </button>
    </div>
  </section>
</template>

<script setup>
import { ref, computed } from "vue";
import portfolioData from "../data/portfolioData.json";

// Résolution des images avec Vite
const getImageUrl = (name) => {
  return new URL(`../assets/${name}`, import.meta.url).href;
};

// Continuous Projects list
const seamlessProjects = computed(() => {
  const list = portfolioData.references || [];
  return [...list, ...list, ...list, ...list];
});

// ÉTATS LOGIQUES & TIMER 2 SECONDES
const isPaused = ref(false);
const isDragging = ref(false);
const startX = ref(0);
const manualOffset = ref(0);
let resumeTimer = null;

// Mettre en pause immédiatement
const pauseAutoScroll = () => {
  if (resumeTimer) clearTimeout(resumeTimer);
  isPaused.value = true;
};

// Reprendre 2 secondes APRÈS avoir quitté le survol
const resumeAutoScrollWithDelay = () => {
  isDragging.value = false;
  if (resumeTimer) clearTimeout(resumeTimer);

  resumeTimer = setTimeout(() => {
    isPaused.value = false;
  }, 1000); // 2000ms = 2 secondes de délai
};

// DRAG & DROP MANUEL
const startDrag = (e) => {
  pauseAutoScroll();
  isDragging.value = true;
  startX.value = e.pageX - manualOffset.value;
};

const stopDragWithDelay = () => {
  resumeAutoScrollWithDelay();
};

const onDrag = (e) => {
  if (!isDragging.value) return;
  e.preventDefault();
  const x = e.pageX;
  manualOffset.value = x - startX.value;
};

// CONTROLE MANUEL FLÈCHES
const scrollManual = (direction) => {
  pauseAutoScroll();
  const step = 410; // 380px + 30px gap
  if (direction === "left") {
    manualOffset.value += step;
  } else {
    manualOffset.value -= step;
  }
  resumeAutoScrollWithDelay();
};

const trackStyle = computed(() => {
  if (isDragging.value || manualOffset.value !== 0) {
    return {
      transform: `translateX(${manualOffset.value}px)`,
      animation: "none",
    };
  }
  return {};
});
</script>

<style scoped>
.reference-section {
  max-width: 100%;
  margin: 0 auto;
  padding: 100px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 30px;
  overflow: hidden;
}

.reference-header {
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
}
.horizontal-lign {
  width: 57px;
  height: 1px;
  margin-top: 10px;
  background-color: var(--color-gold);
}

.slider-wrapper {
  position: relative;
  width: 100%;
  max-width: 1380px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  padding: 0 20px;
}

.slider-container {
  width: 100%;
  overflow: hidden;
  cursor: grab;
  user-select: none;
}

.slider-container:active {
  cursor: grabbing;
}

.slider-track {
  display: flex;
  gap: 30px;
  width: max-content;
  animation: infiniteScroll 90s linear infinite;
}

/* Pause gérée dynamiquement en JS avec le délai de 2s */
.slider-track.is-paused {
  animation-play-state: paused !important;
}

.slider-track.is-dragging {
  animation: none !important;
}

@keyframes infiniteScroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.project-card {
  width: 380px;
  flex-shrink: 0;
  background-color: var(--bg-dark-card);
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  border: 1px solid rgba(255, 255, 255, 0.03);
  transition: background-color 0.4s ease;
}

.project-card:hover {
  background-color: var(--bg-gray-color);
}

.mockup-wrapper {
  width: 100%;
  height: 220px;
  overflow: hidden;
  background-color: #000;
}

.mockup-wrapper img {
  width: 100%;
  height: 100%;
  display: block;
  object-fit: cover;
  pointer-events: none;
}

.project-title-link {
  text-decoration: none;
  width: fit-content;
}

.project-title {
  font-size: 20px;
  color: var(--text-white);
  font-weight: 700;
  transition: color 0.3s ease;
}

.project-title-link:hover .project-title {
  color: var(--color-gold);
}

.project-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

/* BOUTONS FLÈCHES TRANSLUCIDES (Opacité à 30%) */
.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
  background: var(--bg-dark-card);
  color: var(--text-white);
  border: 1px solid rgba(255, 255, 255, 0.2);
  width: 48px;
  height: 48px;
  border-radius: 50%;
  font-size: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  opacity: 0.3; /* Translucide à 30% par défaut */
  transition:
    opacity 0.3s ease,
    background-color 0.3s ease,
    color 0.3s ease;
}

.nav-btn:hover {
  opacity: 1; /* Opacité complète au survol */
  background-color: var(--color-gold);
  color: #000000;
  border-color: var(--color-gold);
}

.btn-left {
  left: 30px;
}

.btn-right {
  right: 30px;
}

@media screen and (max-width: 768px) {
  .project-card {
    width: 300px;
  }
  .nav-btn {
    width: 38px;
    height: 38px;
    font-size: 14px;
  }
  .slider-track {
    gap: 10px;
  }
}
</style>
