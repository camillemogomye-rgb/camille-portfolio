<template>
  <section class="services-section">
    <div class="services-title">
      <h2>DES SERVICES PENSÉS POUR VOTRE SUCCÈS</h2>
      <span class="horizontal-lign"></span>
      <p class="sous-titre">Ce que je propose</p>
    </div>
    <div class="services-cards">
      <div
        class="service-card"
        v-for="service in portfolioData.services"
        :key="service.id"
      >
        <img :src="getImageUrl(service.icone)" :alt="service.icone" />
        <h3>{{ service.titre }}</h3>
        <p class="surtitle">{{ service.surtitre }}</p>
        <p>{{ service.description }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import portfolioData from "../data/portfolioData.json";
const getImageUrl = (name) => {
  return new URL(`../assets/${name}`, import.meta.url).href;
};
</script>

<style scoped>
.services-section {
  display: grid;
  grid-template-columns: 30% 65%;
  gap: 11.37%;
  max-width: 1380px;
  height: calc(100vh - 96px);
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.services-title {
  display: flex;
  flex-direction: column-reverse;
  align-items: flex-start;
  justify-content: flex-end;
  width: 22.68%;
}
.horizontal-lign {
  width: 57px;
  height: 1px;
  margin-top: 10px;
  background-color: var(--color-gold);
}
.services-cards {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  width: 913;
}
.service-card {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  gap: 10px;
  background-color: var(--bg-dark-card);
  padding: clamp(1.25rem, 2.89vw, 2.5rem) 20px;
  border-radius: 0px;
  transition: background-color 0.4s ease;
}
.service-card:hover {
  background-color: #202131;
}
.service-card img {
  width: 60px;
  height: auto;
  object-fit: contain;
}

/*plus petit que tablette*/
@media screen and (max-width: 1024px) {
  .services-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    height: max-content;
  }
  .services-title {
    width: 100%;
    align-items: center;
  }
  .services-title h2 {
    text-align: center;
    padding-top: 10px;
  }
  .services-cards {
    width: 100%;
    gap: 10px;
  }
}
@media screen and (max-width: 768px) {
  .services-cards {
    display: flex;
    flex-direction: column;
  }
  .service-card {
    width: 100%;
    align-items: center;
  }
  .service-card img {
    width: 40px;
  }
  .service-card p {
    text-align: center;
  }
}
</style>
