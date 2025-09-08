<template>
  <div class="team-section" v-if="t">
    <div class="container">
      <h2 class="section-title" id="fundadores">{{ t.foundersTitle }}</h2>
      <div class="team-grid">
        <div
          v-for="member in ownersWithPhotos"
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
              <img
                src="https://cdn-icons-png.flaticon.com/128/6964/6964169.png"
                alt="Ícone de Maleta"
                class="icon-img"
              />
              <span>{{ member.role }}</span>
            </div>
            <div class="detail-item bio-item">
              <img
                src="https://cdn-icons-png.flaticon.com/128/686/686051.png"
                alt="Ícone de Chapéu de Formatura"
                class="icon-img"
              />
              <span>{{ member.bio }}</span>
            </div>
            <div v-if="member.postGrad" class="detail-item postgrad-item">
              <img
                src="https://cdn-icons-png.flaticon.com/128/3000/3000745.png"
                alt="Ícone de Certificado"
                class="icon-img"
              />
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
              <img
                src="https://cdn-icons-png.flaticon.com/128/1384/1384088.png"
                alt="Ícone do LinkedIn"
              />
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, inject, computed } from "vue";

// Importação das imagens para garantir que o Vite as processe corretamente.
import celsoPhoto from "@/assets/celso.png";
import danielPhoto from "@/assets/daniel.png";
import marlonPhoto from "@/assets/marlon.png";

export default defineComponent({
  name: "Sobre",
  setup() {
    // Mapeia os nomes das fotos para os imports reais
    const photoMap: { [key: string]: string } = {
      celsoPhoto,
      danielPhoto,
      marlonPhoto,
    };

    // Injeta os textos traduzidos do componente pai (App.vue)
    const t: any = inject("t");

    // Cria uma propriedade computada que combina os dados de texto com as imagens importadas
    const ownersWithPhotos = computed(() => {
      if (!t || !t.value || !t.value.owners) return [];
      return t.value.owners.map((owner: any) => ({
        ...owner,
        photoUrl: photoMap[owner.photoUrl] || "", // Substitui o nome pela imagem real
      }));
    });

    return {
      t,
      ownersWithPhotos,
    };
  },
});
</script>
