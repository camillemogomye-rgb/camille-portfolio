<template>
  <!-- Conteneur haut (250vh) qui donne la réserve de scroll vertical (Desktop & Responsive) -->
  <div class="scroll-track-container" ref="trackRef">
    <!-- Conteneur figé à l'écran (Sticky 100vh) -->
    <section class="processus-sticky-section">
      <div class="processus-container">
        <!-- En-tête statique -->
        <div class="processus-header">
          <p class="sous-titre">Comment je travaille</p>
          <span class="horizontal-lign"></span>
          <h2>UN PROCESSUS CLAIR, DES RÉSULTATS MESURABLES</h2>
        </div>

        <!-- Chronologie pilotée par le scroll vertical -->
        <div class="timeline-container">
          <!-- Ligne dorée avec dégradé vers les extérieurs -->
          <div class="timeline-line" :style="timelineLineStyle"></div>

          <!-- Grille/Slider des 6 Étapes -->
          <div class="steps-grid" :style="stepsGridStyle">
            <div
              class="step-card"
              v-for="(item, index) in portfolioData.processus"
              :key="index"
              :class="{ 'is-active': isStepActive(index) }"
              :style="getStepStyle(index)"
            >
              <!-- Cercle Numéroté -->
              <div class="step-circle">
                <span>{{ item.step }}</span>
              </div>

              <!-- Contenu Textuel -->
              <div class="step-content">
                <h3 class="step-title">{{ item.titre }}</h3>
                <p class="step-desc">{{ item.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
import portfolioData from "../data/portfolioData.json";

const trackRef = ref(null);
const scrollProgress = ref(0); // Progression de 0 à 1
const windowWidth = ref(window.innerWidth);

const isDesktop = computed(() => windowWidth.value > 1024);

// Calcul du scroll vertical synchronisé
const handleScroll = () => {
  if (!trackRef.value) return;

  const rect = trackRef.value.getBoundingClientRect();
  const windowHeight = window.innerHeight;

  const totalScrollableDistance = rect.height - windowHeight;
  const currentScroll = -rect.top;

  let progress = currentScroll / totalScrollableDistance;
  if (progress < 0) progress = 0;
  if (progress > 1) progress = 1;

  scrollProgress.value = progress;
};

const handleResize = () => {
  windowWidth.value = window.innerWidth;
  handleScroll();
};

// Vérifie si l'étape est active selon la progression du scroll vertical
const isStepActive = (index) => {
  const totalSteps = portfolioData.processus
    ? portfolioData.processus.length
    : 6;
  const stepThreshold = index / (totalSteps - 1);
  return scrollProgress.value >= stepThreshold - 0.08;
};

// Style dynamique de la ligne dorée
const timelineLineStyle = computed(() => {
  if (isDesktop.value) {
    return { transform: `scaleX(${scrollProgress.value})` };
  }
  return {}; // Géré en CSS avec le dégradé sur mobile
});

// Style dynamique du carrousel responsive guidé par le scroll vertical
const stepsGridStyle = computed(() => {
  if (!isDesktop.value) {
    // Fait défiler les cartes horizontalement au fur et à mesure que l'utilisateur scroll vers le bas
    // 6 cartes de 85% + gap : décalage maximal d'environ 80% de la largeur totale du track
    const maxTranslate = 82;
    return {
      transform: `translateX(-${scrollProgress.value * maxTranslate}%)`,
    };
  }
  return {};
});

// Styles dynamiques appliqués pour Desktop
const getStepStyle = (index) => {
  if (!isDesktop.value) return {};

  const totalSteps = portfolioData.processus
    ? portfolioData.processus.length
    : 6;
  const stepStart = index / (totalSteps - 1);

  let opacity = 0;
  if (scrollProgress.value >= stepStart) {
    opacity = 1;
  } else {
    opacity = Math.max(0, (scrollProgress.value - (stepStart - 0.15)) / 0.15);
  }

  return {
    opacity: opacity,
    transform: `translateY(${(1 - opacity) * 20}px)`,
    transition: "opacity 0.2s ease-out, transform 0.2s ease-out",
  };
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll, { passive: true });
  window.addEventListener("resize", handleResize);
  handleScroll();
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
  window.removeEventListener("resize", handleResize);
});
</script>

<style scoped>
/* Conteneur très haut qui donne la réserve de scroll vertical */
.scroll-track-container {
  position: relative;
  height: 250vh;
}

/* Zone figée à l'écran pendant toute la durée du scroll vertical */
.processus-sticky-section {
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.processus-container {
  width: 100%;
  max-width: 1380px;
  padding: 0 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 60px;
}

.processus-header {
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 12px;
  align-items: center;
  max-width: 1005px;
}

.horizontal-lign {
  width: 57px;
  height: 1px;
  margin-top: 10px;
  background-color: var(--color-gold);
}

.timeline-container {
  position: relative;
  width: 100%;
  padding-top: 20px;
}

/* Ligne dorée Desktop */
.timeline-line {
  position: absolute;
  top: 45px;
  left: 0;
  height: 1px;
  background: var(--color-gold);
  width: 100%;
  z-index: 1;
  transform-origin: left;
  will-change: transform;
  transition: transform 0.1s linear;
}

.steps-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 20px;
  position: relative;
  z-index: 2;
  will-change: transform;
}

.step-card {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 20px;
  will-change: opacity, transform;
}

.step-circle {
  width: clamp(2.5rem, 4vw, 3.5rem);
  height: clamp(2.5rem, 4vw, 3.5rem);
  border-radius: 50%;
  background-color: var(--bg-dark-main);
  border: 1px solid var(--color-gold);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-white);
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  font-size: clamp(1rem, 1.4vw, 1.25rem);
  transition: all 0.3s ease;
}

.step-card.is-active .step-circle {
  border-color: var(--color-gold);
  background-color: var(--bg-dark-card);
  color: var(--color-white);
}

.step-card.is-active:hover .step-circle {
  border-color: var(--color-gold);
  color: #000000;
  background-color: var(--color-gold);
  box-shadow: 0 0 18px rgba(241, 236, 76, 0.4);
}

.steps-grid:hover .step-card {
  opacity: 0.8 !important;
  filter: blur(0.5px);
  transition:
    opacity 2s ease-in-out,
    filter 2s ease-in-out,
    transform 2s ease-in-out;
}

/* C. La carte PRÉCISÉMENT SURVOLÉE reprend 100% d'opacité, retire son flou, grandit et passe au-dessus */
.steps-grid .step-card:hover {
  opacity: 1 !important;
  filter: blur(0px) !important;
  transform: translateY(3px) scale(1.02) !important;
  z-index: 10; /* Passe au-dessus pour que le halo doré ne soit pas masqué */
}

.step-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.step-title {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-muted);
  transition: color 0.3s ease;
}

.step-card.is-active .step-title {
  color: var(--color-gold);
}

.step-desc {
  color: var(--text-muted);
  line-height: 1.5;
  transition: color 0.3s ease;
}

.step-card.is-active .step-desc {
  color: var(--text-white);
}

/* --- RESPONSIVE SPECS : TABLETTE & MOBILE --- */
@media screen and (max-width: 1024px) {
  .processus-container {
    padding: 0 10px;
    gap: 5px;
  }

  .timeline-container {
    overflow: hidden;
    padding: 30px 0;
  }

  /* 1. LIGNE GOLD AVEC DÉGRADÉ FONDU VERS LES EXTÉRIEURS */
  .timeline-line {
    top: 52px;
    height: 1px;
    background: var(--color-gold);
    /* Dégradé de transparence sur les côtés gauche et droit */
    -webkit-mask-image: linear-gradient(
      to right,
      transparent 0%,
      black 20%,
      black 80%,
      transparent 100%
    );
    mask-image: linear-gradient(
      to right,
      transparent 0%,
      black 20%,
      black 80%,
      transparent 100%
    );
    opacity: 0.6;
    transform: none !important;
  }

  /* 2. CARROUSEL SCROLL-DRIVEN (PILOTÉ PAR LE SCROLL VERTICAL) */
  .steps-grid {
    display: flex !important;
    grid-template-columns: none !important;
    width: max-content;
    padding-left: 7.5vw; /* Centre la première carte à 85% */
    gap: 30px;
    transition: transform 0.15s cubic-bezier(0.1, 0.2, 0.2, 1);
  }

  /* 3. L'ÉTAPE OCCUPE EXACTEMENT 85% DE LA LARGEUR RESPONSIVE */
  .step-card {
    flex: 0 0 70vw !important;
    width: 70vw !important;
    opacity: 0.35 !important;
    transform: scale(0.9) !important;
    transition:
      transform 0.3s ease,
      opacity 0.3s ease;
  }

  /* Carte active mise en valeur au centre */
  .step-card.is-active {
    opacity: 1 !important;
    transform: scale(1) !important;
  }
}

@media screen and (max-width: 640px) {
  .timeline-line {
    top: 48px;
  }
}
</style>
