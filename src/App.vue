<template>
  <div class="app-container">
    <!-- Grille de lignes verticales en arrière-plan -->
    <div class="bg-lines-grid">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>

    <TheHeader />

    <main class="main-container">
      <HeroSection />
      <ServicesSection />
      <ReferenceSection />
      <ProcessusSection />
    </main>
  </div>
</template>

<script setup>
import TheHeader from "./components/TheHeader.vue";
import HeroSection from "./components/HeroSection.vue";
import ServicesSection from "./components/ServicesSection.vue";
import ReferenceSection from "./components/ReferenceSection.vue";
import ProcessusSection from "./components/ProcessusSection.vue";
</script>

<style>
.main-container {
  padding-top: 96px;
  min-height: 100vh;
  max-width: 100%;
  margin: 0 auto;
}

.bg-lines-grid {
  position: fixed;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  max-width: 1380px;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  pointer-events: none;
  z-index: -1;
  padding: 0 20px;
}

.bg-lines-grid span:first-child {
  border-left: 1px solid rgba(255, 255, 255, 0.08);
}

.bg-lines-grid span {
  height: 100%;
  border-right: 1px solid rgba(255, 255, 255, 0.08);
}

@media screen and (max-width: 1024px) {
  .main-container {
    padding-top: 120px;
  }
}
@media screen and (max-width: 768px) {
}
</style>
