<template>
  <section id="apropos" class="contact-section" ref="contactRef">
    <div class="contact-container">
      <!-- TITRE AVEC EFFET MACHINE À ÉCRIRE (À DROITE) -->
      <div class="contact-text-wrapper">
        <p class="sous-titre">Parlons de votre projet</p>
        <span class="horizontal-lign"></span>
        <h2 class="typewriter-title">
          {{ displayText }}<span class="cursor" v-if="isTyping">|</span>
        </h2>
      </div>
      <!-- FORMULAIRE (À GAUCHE) -->
      <div class="contact-form-wrapper">
        <form @submit.prevent="sendEmail" class="contact-form">
          <div class="form-row">
            <div class="input-group">
              <input
                type="text"
                v-model="formData.nom"
                placeholder="Nom *"
                required
              />
            </div>
            <div class="input-group">
              <input
                type="text"
                v-model="formData.prenom"
                placeholder="Prénom *"
                required
              />
            </div>
          </div>

          <div class="form-row">
            <div class="input-group">
              <input
                type="tel"
                v-model="formData.telephone"
                placeholder="Téléphone *"
                required
              />
            </div>
            <div class="input-group">
              <input
                type="email"
                v-model="formData.email"
                placeholder="E-mail *"
                required
              />
            </div>
          </div>

          <div class="input-group full-width">
            <select v-model="formData.service" required>
              <option value="" disabled selected>
                Sélectionner un service *
              </option>
              <option value="Création de site internet">
                Création de site internet
              </option>
              <option value="Design UI/UX">Design UI/UX</option>
              <option value="Optimisation SEO">Optimisation SEO</option>
              <option value="Gestion de projet IT">Gestion de projet IT</option>
            </select>
          </div>

          <div class="input-group full-width">
            <textarea
              v-model="formData.message"
              placeholder="Votre message *"
              rows="5"
              required
            ></textarea>
          </div>

          <button
            type="submit"
            class="bouton bouton-gold"
            :disabled="isSending"
          >
            <span v-if="!isSending">DEVIS GRATUIT</span>
            <span v-else>ENVOI EN COURS...</span>
          </button>

          <!-- Feedback message -->
          <p v-if="statusMessage" :class="['status-msg', statusType]">
            {{ statusMessage }}
          </p>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from "vue";
import emailjs from "@emailjs/browser";

// --- GESTION DU FORMULAIRE ---
const formData = reactive({
  nom: "",
  prenom: "",
  telephone: "",
  email: "",
  service: "",
  message: "",
});

const isSending = ref(false);
const statusMessage = ref("");
const statusType = ref("");

// IDENTIFIANTS EMAILJS (À remplacer après création de ton compte gratuit)
const SERVICE_ID = "YOUR_SERVICE_ID";
const TEMPLATE_ID_ADMIN = "YOUR_TEMPLATE_ID_ADMIN"; // Envoi vers camillemogomye@gmail.com
const PUBLIC_KEY = "YOUR_PUBLIC_KEY";

const sendEmail = async () => {
  isSending.value = true;
  statusMessage.value = "";

  try {
    // 1. Envoi de la notification vers camillemogomye@gmail.com
    await emailjs.send(
      SERVICE_ID,
      TEMPLATE_ID_ADMIN,
      {
        from_name: `${formData.prenom} ${formData.nom}`,
        from_email: formData.email,
        phone: formData.telephone,
        service: formData.service,
        message: formData.message,
        to_email: "camillemogomye@gmail.com",
      },
      PUBLIC_KEY,
    );

    statusMessage.value =
      "Votre message a été envoyé avec succès ! Un e-mail de confirmation vous a été adressé.";
    statusType.value = "success";

    // Réinitialisation du formulaire
    Object.keys(formData).forEach((key) => (formData[key] = ""));
  } catch (error) {
    console.error("EmailJS Error:", error);
    statusMessage.value =
      "Une erreur est survenue lors de l'envoi. Veuillez réessayer.";
    statusType.value = "error";
  } finally {
    isSending.value = false;
  }
};

// --- ANIMATION TYPEWRITER (MACHINE À ÉCRIRE) ---
const fullText = "PRÊT À CRÉER QUELQUE CHOSE D'EXCEPTIONNEL ?";
const displayText = ref("");
const isTyping = ref(false);
const contactRef = ref(null);
let typeIndex = 0;
let observer = null;

const startTypewriter = () => {
  if (isTyping.value) return;
  isTyping.value = true;
  displayText.value = "";
  typeIndex = 0;

  const interval = setInterval(() => {
    if (typeIndex < fullText.length) {
      displayText.value += fullText.charAt(typeIndex);
      typeIndex++;
    } else {
      clearInterval(interval);
      isTyping.value = false;
    }
  }, 60); // Vitesse de frappe (60ms par lettre)
};

onMounted(() => {
  // Déclenchement de la machine à écrire au scroll quand la section apparaît
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        startTypewriter();
      }
    },
    { threshold: 0.3 },
  );

  if (contactRef.value) {
    observer.observe(contactRef.value);
  }
});

onUnmounted(() => {
  if (observer) observer.disconnect();
});
</script>

<style scoped>
.contact-section {
  max-width: 1380px;
  margin: 0 auto;
  gap: clamp(1.25rem, 5.79vw, 5rem);
  min-height: calc(100vh - 96px);
  display: flex;
}

.contact-container {
  display: flex;
  justify-content: space-between;
  align-items: stretch;
  gap: clamp(1.25rem, 5.79vw, 5rem);
  height: 70vh;
}

.contact-form-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: flex-end; /* Aligne tout le formulaire en bas */
  align-items: flex-end; /* Calé à droite */
  width: 50%; /* Largeur pour le formulaire */
  order: 2; /* Place le formulaire en second (à droite) */
}

/* --- FORMULAIRE --- */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  width: 100%;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}

.input-group input,
.input-group select,
.input-group textarea {
  width: 100%;
  background-color: var(--bg-gray-color);
  border: 1px solid var(--bg-gray-color);
  padding: 10px 20px;
  color: var(--text-white);
  font-family: var(--font-body);
  font-size: clamp(1rem, 1.449vw, 1.25rem);
  font-weight: 200;
  outline: none;
  transition: border-color 0.3s ease;
}

.input-group input:focus,
.input-group select:focus,
.input-group textarea:focus {
  border-color: var(--color-white);
}

.input-group select {
  appearance: none;
  cursor: pointer;
  background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='white'%3e%3cpath d='M7 10l5 5 5-5z'/%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-position: right 15px center;
  background-size: 20px;
}

.bouton-gold {
  background-color: var(--color-gold);
  color: #000000;
  border: none;
  font-weight: 700;
  cursor: pointer;
  padding: 18px 36px;
  width: fit-content;
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.bouton-gold:hover {
  opacity: 0.9;
  transform: translateY(-2px);
}

.status-msg {
  font-size: 14px;
  margin-top: 10px;
}

.status-msg.success {
  color: #4ade80;
}

.status-msg.error {
  color: #f87171;
}

/* --- TEXTE ET MACHINE À ÉCRIRE --- */
.contact-text-wrapper {
  display: flex;
  flex-direction: column;
  width: 60%;
  gap: 15px;
}

.horizontal-lign {
  width: 57px;
  height: 1px;
  background-color: var(--bg-gray-color);
}

.typewriter-title {
  min-height: 150px; /* Évite les sauts de hauteur pendant l'animation */
}

.cursor {
  color: var(--color-white);
  animation: blink 2s infinite;
}

@keyframes blink {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}

/* RESPONSIVE */
@media screen and (max-width: 1024px) {
  .contact-container {
    flex-direction: column;
    height: auto;
    gap: 20px;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 10px;
  }
  .contact-text-wrapper,
  .contact-form-wrapper {
    width: 100%;
    order: initial;
    justify-content: flex-start;
    align-items: flex-start;
  }
  .contact-form {
    gap: 10px;
  }
  .typewriter-title {
    min-height: auto;
  }
}
</style>
