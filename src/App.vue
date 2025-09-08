<script setup lang="ts">
import { ref, onMounted } from "vue";
import Sobre from "@/components/Sobre.vue";
import logoUrl from "./assets/logo.png";

// Gerencia o estado de abertura do menu de navegação em dispositivos móveis.
const isMenuOpen = ref(false);

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}
function closeMenu() {
  isMenuOpen.value = false;
}

// Define os dados para a seção de portfólio, que serão renderizados dinamicamente.
const portfolio = ref([
  {
    client: "Empresa de Logística Exemplo",
    logo: "https://via.placeholder.com/150/2DA9B0/FFFFFF?text=Logo",
    description:
      "Desenvolvemos um sistema de gerenciamento de frotas e otimização de rotas em tempo real, resultando em uma redução de 15% nos custos operacionais e um aumento de 20% na eficiência das entregas.",
    link: "https://example.com",
    linkText: "Ver Estudo de Caso",
  },
  {
    client: "Clínica Médica Exemplo",
    logo: "https://via.placeholder.com/150/3E4A59/FFFFFF?text=Logo",
    description:
      "Implementação de um sistema de agendamento online e prontuário eletrônico (PWA), melhorando a experiência do paciente e centralizando as informações de forma segura e acessível para os profissionais de saúde.",
    link: null,
    linkText: "Projeto de Sistema Interno",
  },
]);

// Cria uma diretiva customizada (v-fade-in) para aplicar animações de fade-in aos elementos quando eles entram na tela.
const vFadeIn = {
  mounted: (el: HTMLElement) => {
    el.classList.add("fade-in");

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            el.classList.add("visible");
            observer.unobserve(el);
          }
        });
      },
      { threshold: 0.15 }
    );

    observer.observe(el);
  },
};
</script>

<template>
  <header id="header">
    <nav class="container">
      <a href="#hero" class="logo-link" @click="closeMenu">
        <img src="./assets/logo.png" alt="CDM IT Logo" class="logo" />
      </a>
      <button
        class="hamburger"
        @click="toggleMenu"
        :class="{ 'is-active': isMenuOpen }"
        aria-label="Menu"
        aria-controls="navigation"
        :aria-expanded="isMenuOpen"
      >
        <span class="line"></span>
        <span class="line"></span>
        <span class="line"></span>
      </button>
      <ul
        class="nav-links"
        :class="{ 'nav-active': isMenuOpen }"
        id="navigation"
      >
        <li><a href="#about" @click="closeMenu">Sobre</a></li>
        <li><a href="#fundadores" @click="closeMenu">Fundadores</a></li>
        <li><a href="#services" @click="closeMenu">Serviços</a></li>
        <li><a href="#portfolio" @click="closeMenu">Projetos</a></li>
        <li><a href="#contact" @click="closeMenu">Contato</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="hero">
      <div class="hero-content container">
        <h1>Construindo o Futuro do Seu Negócio</h1>
        <p class="subtitle">
          Software Personalizado, Infraestrutura Robusta e Consultoria
          Especializada em TI
        </p>
        <a href="#services" class="cta-button">Explore Nossos Serviços</a>
      </div>
    </section>

    <section id="about" v-fade-in>
      <div class="container">
        <h2>Sobre a CDM</h2>
        <div class="about-logo-container">
          <img :src="logoUrl" alt="Logo da CDM" class="about-logo" />
        </div>
        <p>
          Fundada por <strong>Celso, Daniel e Marlon</strong>, a CDM Soluções em
          TI se dedica a capacitar pequenas e médias empresas através da
          tecnologia. Acreditamos na construção de parcerias sólidas,
          compreendendo seus desafios únicos e entregando soluções
          personalizadas que impulsionam o crescimento, a eficiência e a
          inovação. Nossa experiência combinada é o seu trunfo para navegar no
          cenário digital.
        </p>
      </div>
      <Sobre />
    </section>

    <section id="services" v-fade-in>
      <div class="container">
        <h2>Nossos Principais Serviços</h2>
        <div class="services-grid">
          <div class="service-card">
            <div class="service-icon">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="48"
                height="48"
                fill="currentColor"
                viewBox="0 0 256 256"
              >
                <path
                  d="M88,144,32,88,88,32"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></path>
                <path
                  d="M168,224,224,168,168,112"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></path>
                <line
                  x1="152"
                  y1="32"
                  x2="104"
                  y2="224"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></line>
              </svg>
            </div>
            <h3>Desenvolvimento Personalizado</h3>
            <p>
              Construímos soluções digitais escaláveis e intuitivas, incluindo
              sites dinâmicos, progressive web apps (PWAs), sistemas de ponto de
              venda e aplicações de negócios personalizadas para suas
              necessidades operacionais específicas.
            </p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="48"
                height="48"
                fill="currentColor"
                viewBox="0 0 256 256"
              >
                <rect
                  x="40"
                  y="88"
                  width="176"
                  height="80"
                  rx="8"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></rect>
                <line
                  x1="176"
                  y1="168"
                  x2="176"
                  y2="208"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></line>
                <line
                  x1="80"
                  y1="168"
                  x2="80"
                  y2="208"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></line>
                <line
                  x1="128"
                  y1="88"
                  x2="128"
                  y2="48"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></line>
                <line
                  x1="40"
                  y1="128"
                  x2="16"
                  y2="128"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></line>
                <line
                  x1="216"
                  y1="128"
                  x2="240"
                  y2="128"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></line>
              </svg>
            </div>
            <h3>Infraestrutura de TI</h3>
            <p>
              Projetamos e gerenciamos ambientes de TI robustos. Nossos serviços
              incluem instalação de redes, sistemas de controle de acesso seguro
              (biometria, facial), configuração de servidores e monitoramento
              contínuo para garantir o desempenho ideal.
            </p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="48"
                height="48"
                fill="currentColor"
                viewBox="0 0 256 256"
              >
                <path
                  d="M128,72a56,56,0,1,0,56,56A56.06,56.06,0,0,0,128,72Zm0,96a40,40,0,1,1,40-40A40.05,40.05,0,0,1,128,168Z"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></path>
                <path
                  d="M68.61,196.61A95.49,95.49,0,0,1,32,128a95.49,95.49,0,0,1,36.61-68.61"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></path>
                <path
                  d="M187.39,59.39A95.49,95.49,0,0,1,224,128a95.49,95.49,0,0,1-36.61,68.61"
                  fill="none"
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="20"
                ></path>
              </svg>
            </div>
            <h3>Consultoria Especializada</h3>
            <p>
              Aproveite nossa experiência para tomar decisões tecnológicas
              informadas. Oferecemos orientação estratégica em desenvolvimento,
              infraestrutura e redes para alinhar sua estratégia de TI com seus
              objetivos de negócios para o sucesso a longo prazo.
            </p>
          </div>
        </div>
      </div>
    </section>

    <section id="portfolio" v-fade-in>
      <div class="container">
        <h2>Nosso Portfólio</h2>
        <div class="portfolio-list">
          <div
            v-for="project in portfolio"
            :key="project.client"
            class="portfolio-card"
          >
            <div class="portfolio-logo-wrapper">
              <img
                :src="project.logo"
                :alt="'Logo ' + project.client"
                class="portfolio-logo"
              />
            </div>
            <div class="portfolio-info">
              <h3>{{ project.client }}</h3>
              <p>{{ project.description }}</p>
              <a
                v-if="project.link"
                :href="project.link"
                target="_blank"
                rel="noopener noreferrer"
                class="portfolio-link"
                >{{ project.linkText }} &rarr;</a
              >
              <span v-else class="portfolio-tag">{{ project.linkText }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="contact" v-fade-in>
      <div class="container">
        <h2>Pronto para Elevar o Seu Negócio?</h2>
        <p>
          Vamos conversar sobre como nossas soluções de TI podem ajudá-lo a
          alcançar seus objetivos. Entre em contato hoje para uma consulta.
        </p>
        <a href="https://wa.me/5511987654321" class="cta-button" target="_blank"
          >Entre em Contato</a
        >
      </div>
    </section>
  </main>

  <footer>
    <div class="container">
      <p>&copy; 2025 CDM Soluções em TI. Todos os Direitos Reservados.</p>
    </div>
  </footer>
</template>
