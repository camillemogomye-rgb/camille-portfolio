<template>
  <header class="site-header">
    <div class="header-container">
      <div class="logo-container">
        <img src="../assets/logo.svg" alt="Logo" />
      </div>
      <nav>
        <ul>
          <li><a href="#accueil">ACCUEIL</a></li>
          <li><a href="#services">SERVICES</a></li>
          <li><a href="#portfolio">PORTFOLIO</a></li>
          <li><a href="#processus">PROCESSUS</a></li>
          <li><a href="#apropos">À PROPOS</a></li>
        </ul>
      </nav>
      <div class="bouton-container">
        <a>DEVIS GRATUIT</a>
      </div>
    </div>
  </header>
</template>

<script setup></script>

<style scoped>
.site-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: var(--bg-dark-card);
  z-index: 999;
}

.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  max-width: 1380px;
  align-items: center;
  margin: 0 auto;
  padding: 20px;
}

nav ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 30px;
}

nav a {
  color: var(--text-white);
  text-decoration: none;
  transition: color 0.3s ease;
}

nav a:hover {
  color: var(--color-gold);
}

.bouton-container {
  background-color: var(--color-gold);
  color: var(--bg-dark-card);
  padding: 12px 38px;
  border: 1px solid var(--color-gold);
  transition: background-color 0.3s ease;
  text-decoration: none;
  display: inline-block;
  margin-left: 20px;
}

.bouton-container:hover {
  background-color: var(--bg-dark-card);
  color: var(--color-gold);
  border: 1px solid var(--color-gold);
}

@media screen and (max-width: 768px) {
  nav {
    display: none;
  }

  .logo-container img {
    width: 80%;
  }
}
</style>
