<!-- Estrutura visual do componente Sobre -->
<template>
  <div class="team-section">
    <div class="container">
      <h2 class="section-title" id="fundadores">Nossos Fundadores</h2>
      <div class="team-grid">
        <div
          v-for="member in owners"
          :key="member.name"
          class="team-member-card"
        >
          <div class="member-photo-wrapper">
            <img
              :src="member.photoUrl"
              :alt="'Foto de ' + member.name"
              class="member-photo"
            />
          </div>
          <h3 class="member-name">{{ member.name }}</h3>
          <div class="member-details">
            <div class="detail-item role-item">
              <div class="icon-wrapper">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  fill="currentColor"
                  viewBox="0 0 256 256"
                >
                  <rect
                    x="32"
                    y="72"
                    width="192"
                    height="144"
                    rx="8"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></rect>
                  <path
                    d="M176,72V56a24,24,0,0,0-24-24H104A24,24,0,0,0,80,56v16"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></path>
                </svg>
              </div>
              <span>{{ member.role }}</span>
            </div>
            <div class="detail-item bio-item">
              <div class="icon-wrapper">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  fill="currentColor"
                  viewBox="0 0 256 256"
                >
                  <path
                    d="M24,96,128,40,232,96v64a16,16,0,0,1-16,16H40a16,16,0,0,1-16-16Z"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></path>
                  <path
                    d="M208,96v88a16,16,0,0,1-16,16H64a16,16,0,0,1-16-16V96"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></path>
                </svg>
              </div>
              <span>{{ member.bio }}</span>
            </div>
            <div v-if="member.postGrad" class="detail-item postgrad-item">
              <div class="icon-wrapper">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  fill="currentColor"
                  viewBox="0 0 256 256"
                >
                  <path
                    d="M184,224l-32-32,32-32"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></path>
                  <path
                    d="M80,128a48,48,0,1,0,48,48,48.05,48.05,0,0,0-48-48Z"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></path>
                  <path
                    d="M128,32a96,96,0,1,0,96,96,96.11,96.11,0,0,0-96-96Zm0,160a64,64,0,1,1,64-64A64.07,64.07,0,0,1,128,192Z"
                    fill="none"
                    stroke="currentColor"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="16"
                  ></path>
                </svg>
              </div>
              <span>{{ member.postGrad }}</span>
            </div>
          </div>
          <div class="member-socials">
            <a
              :href="member.linkedinUrl"
              target="_blank"
              rel="noopener noreferrer"
              class="social-link"
              title="Ver perfil no LinkedIn"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                fill="currentColor"
                viewBox="0 0 256 256"
              >
                <path
                  d="M216,24H40A16,16,0,0,0,24,40V216a16,16,0,0,0,16,16H216a16,16,0,0,0,16-16V40A16,16,0,0,0,216,24Zm0,192H40V40H216V216ZM96,112v64a8,8,0,0,1-16,0V112a8,8,0,0,1,16,0Zm88,28v36a8,8,0,0,1-16,0V140a20,20,0,0,0-40,0v36a8,8,0,0,1-16,0V112a8,8,0,0,1,15.79-1.75A36,36,0,0,1,184,140ZM84,80a12,12,0,1,1-12-12A12,12,0,0,1,84,80Z"
                ></path>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<!-- Lógica e dados do componente -->
<script lang="ts">
import { defineComponent } from "vue";

// Importação das imagens para garantir que o Vite as processe corretamente durante o build.
import celsoPhoto from "@/assets/celso.png";
import danielPhoto from "@/assets/daniel.png";
import marlonPhoto from "@/assets/marlon.png";

export default defineComponent({
  name: "Sobre",
  setup() {
    const owners = [
      {
        name: "Celso Rodrigo Giusti",
        role: "Especialista em Infraestrutura e Redes",
        photoUrl: celsoPhoto,
        linkedinUrl: "https://www.linkedin.com/in/celso-giusti-886b8596",
        bio: "Graduado em Análise e desenvolvimento de sistemas pela FPM e Gestão Empresarial pela FATEC.",
      },
      {
        name: "Daniel Manoel Filho",
        role: "Especialista em Desenvolvimento de Software",
        photoUrl: danielPhoto,
        linkedinUrl: "https://www.linkedin.com/in/dannmf",
        bio: "Graduado em Análise e Desenvolvimento de Sistemas pela FATEC.",
      },
      {
        name: "Marlon Palata Fanger Rodrigues",
        role: "Especialista em Segurança da Informação",
        photoUrl: marlonPhoto,
        linkedinUrl: "https://www.linkedin.com/in/marlonfangerrodrigues",
        bio: "Graduado em Redes de Computadores e Análise e Desenvolvimento de Sistemas pela FATEC Indaiatuba.",
        postGrad:
          "Pós-graduado em Segurança da Informação pela faculdade Líbano.",
      },
    ];

    return {
      owners,
    };
  },
});
</script>
