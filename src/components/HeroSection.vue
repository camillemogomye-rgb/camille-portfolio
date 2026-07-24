<template>
  <section id="accueil" class="hero-section">
    <div class="hero-container">
      <p class="text-container">Hello, je suis</p>
      <h1 class="hero-title">
        WEBDESIGNER SENIOR <br />
        <span class="hero-subtitle">ET CHEF PROJET DIGITAL.</span>
      </h1>
      <div class="hero-content">
        <div class="hero-description">
          <div class="nom-profession">
            <p class="nom">CAMILLE FLORENT D.M.</p>
            <p class="profession">
              Webdesigner Senior · Digital Project Manager
            </p>
          </div>
          <img
            class="separateur"
            src="../assets/Ligne ondulee.svg"
            alt="Séparateur"
          />
          <div class="skills">
            <p class="skill">Adobe XD</p>
            <p class="skill">WordPress</p>
            <p class="skill">Elementor</p>
            <p class="skill">UX/UI</p>
            <p class="skill">Gestion de projet</p>
            <p class="skill">SEO</p>
          </div>
        </div>
        <div class="description">
          <p>
            Je transforme vos idées en sites web professionnels qui attirent,
            convainquent et convertissent. Design sur mesure, intégration
            WordPress et gestion de projet rigoureuse — de la maquette à la mise
            en ligne.
          </p>
          <div class="bouton-container">
            <a class="bouton-white">DEVIS GRATUIT</a>
            <a class="bouton-outline">CONSULTER MON CV</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup></script>

<style scoped>
.hero-section {
  max-width: 1380px;
  margin: 0 auto;
  padding: 40px 20px;
  height: calc(100vh - 128px);
}

.text-container {
  font-size: 30px;
  line-height: 39px;
  color: var(--text-white);
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.hero-title {
  font-size: 100px;
  line-height: 100px;
  color: var(--color-gold);
  text-align: center;
  width: 100%;
}
.hero-subtitle {
  font-size: 68px;
  line-height: 70px;
  color: var(--text-white);
  margin-top: -20px;
}
.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  row-gap: 40px;
  margin-top: 40px;
  width: 90%;
}
.hero-description {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-color: var(--bg-dark-card);
  padding: 48px 70px;
  gap: 20px;
  width: 577px;
}
.nom-profession {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.nom {
  font-size: 20px;
  line-height: 26px;
  color: var(--text-white);
}
.profession {
  font-size: 20px;
  line-height: 26px;
  color: var(--color-gold);
}
.separateur {
  width: 70%;
}
.skills {
  display: flex;
  flex-direction: row;
  gap: 10px 22px;
  flex-wrap: wrap;
}
.skill {
  background-color: #202131;
  border: 0.5px solid #707070;
  border-radius: 50px;
  padding: 4px 12px;
  font-size: 16px;
  line-height: 21px;
  color: var(--text-white);
}
.description {
  padding: 0px;
  display: flex;
  flex-direction: column;
  justify-content: content;
}
.bouton-container {
  display: flex;
  flex-direction: row;
  gap: 24px;
  margin-top: 20px;
}
.bouton-white {
  background-color: var(--text-white);
  border: 1px solid var(--text-white);
  border-radius: 0px;
  padding: 21px 50px;
  font-size: 20px;
  line-height: 26px;
  color: var(--bg-dark-card);
  text-align: center;
}
.bouton-outline {
  background-color: transparent;
  border: 1px solid var(--text-white);
  border-radius: 0px;
  padding: 21px 50px;
  font-size: 20px;
  line-height: 26px;
  color: var(--text-white);
  text-align: center;
}
</style>
