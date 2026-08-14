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
            <a class="bouton bouton-white">DEVIS GRATUIT</a>
            <a class="bouton bouton-outline">CONSULTER MON CV</a>
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
  height: calc(100vh - 96px);
  margin: 0 auto;
  display: flex;
  align-items: center;
}

.text-container {
  font-size: clamp(1.25rem, 2.17vw, 1.875rem);
  line-height: 1.3088;
  color: var(--text-white);
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.hero-title {
  color: var(--color-gold);
  text-align: center;
  width: 100%;
}
.hero-subtitle {
  font-size: clamp(1.56rem, 4.9vw, 4.25rem);
  line-height: 1.3088;
  color: var(--text-white);
  margin-top: -20px;
}
.hero-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  margin-top: 40px;
  width: 90%;
}
.hero-description {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-color: var(--bg-dark-card);
  padding: clamp(1.25rem, 3.76vw, 3.25rem) clamp(1.56rem, 5.72vw, 4.93rem);
  gap: 20px;
  position: relative;
  width: 100%;
}
.nom-profession {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.nom {
  font-weight: bold;
  color: var(--text-white);
}
.profession {
  font-weight: bold;
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

.description {
  padding: 0px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.bouton-container {
  display: flex;
  flex-direction: row;
  gap: 24px;
  margin-top: 20px;
}

@media screen and (max-width: 1024px) {
  .hero-content {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 100%;
    margin-top: 20px;
  }
  .nom {
    text-align: center;
  }
  .profession {
    text-align: center;
  }
  .hero-description {
    align-items: center;
  }
  .skills {
    justify-content: center;
    gap: 10px 20px;
    flex-wrap: wrap;
  }
  .description p {
    text-align: center;
  }
  .bouton-container {
    justify-content: center;
  }
}
</style>
