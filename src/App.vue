<script setup lang="ts">
import {
  ref,
  onMounted,
  onUnmounted,
  computed,
  watchEffect,
  provide,
} from "vue";
import Sobre from "@/components/Sobre.vue";
import logoUrl from "./assets/logo.png";

// --- GERENCIAMENTO DE TEMA ---
const theme = ref(localStorage.getItem("theme") || "system");
const isSystemDark = ref(
  window.matchMedia("(prefers-color-scheme: dark)").matches
);

const effectiveTheme = computed(() => {
  if (theme.value === "system") {
    return isSystemDark.value ? "dark" : "light";
  }
  return theme.value;
});

watchEffect(() => {
  const root = document.documentElement;
  if (effectiveTheme.value === "dark") {
    root.classList.add("dark");
  } else {
    root.classList.remove("dark");
  }
  if (theme.value !== "system") {
    localStorage.setItem("theme", theme.value);
  }
});

onMounted(() => {
  const mediaQuery = window.matchMedia("(prefers-color-scheme: dark)");
  const updateSystemTheme = (e: MediaQueryListEvent) =>
    (isSystemDark.value = e.matches);
  mediaQuery.addEventListener("change", updateSystemTheme);
  onUnmounted(() =>
    mediaQuery.removeEventListener("change", updateSystemTheme)
  );
});

function toggleTheme() {
  theme.value = effectiveTheme.value === "light" ? "dark" : "light";
}

// --- GERENCIAMENTO DE IDIOMA ---
const language = ref<"pt" | "en">("pt"); // CORREÇÃO: Tipagem explícita para resolver erro de índice.
const translations = ref({
  pt: {
    // Top Bar & Header
    followUs: "Sigam-nos nas redes sociais",
    logoAlt: "Logo da CDM IT",
    navAbout: "Sobre",
    navFounders: "Fundadores",
    navServices: "Serviços",
    navProjects: "Projetos",
    navContact: "Contato",
    // Hero Section
    heroTitle: "Construindo o Futuro do Seu Negócio",
    heroSubtitle:
      "Software Personalizado, Infraestrutura Robusta e Consultoria Especializada em TI",
    heroButton: "Explore Nossos Serviços",
    // About Section
    aboutTitle: "Sobre a CDM",
    aboutText:
      "Fundada por <strong>Celso, Daniel e Marlon</strong>, a CDM Soluções em TI se dedica a capacitar pequenas e médias empresas através da tecnologia. Acreditamos na construção de parcerias sólidas, compreendendo seus desafios únicos e entregando soluções personalizadas que impulsionam o crescimento, a eficiência e a inovação. Nossa experiência combinada é o seu trunfo para navegar no cenário digital.",
    // Founders Section (for Sobre.vue)
    foundersTitle: "Nossos Fundadores",
    owners: [
      {
        name: "Celso Rodrigo Giusti",
        role: "Especialista em Infraestrutura e Redes",
        photoUrl: "celsoPhoto",
        linkedinUrl: "https://www.linkedin.com/in/celso-giusti-886b8596",
        bio: "Graduado em Análise e desenvolvimento de sistemas pela FPM e Gestão Empresarial pela FATEC.",
      },
      {
        name: "Daniel Manoel Filho",
        role: "Especialista em Desenvolvimento de Software",
        photoUrl: "danielPhoto",
        linkedinUrl: "https://www.linkedin.com/in/dannmf",
        bio: "Graduado em Análise e Desenvolvimento de Sistemas pela FATEC.",
      },
      {
        name: "Marlon Palata Fanger Rodrigues",
        role: "Especialista em Segurança da Informação",
        photoUrl: "marlonPhoto",
        linkedinUrl: "https://www.linkedin.com/in/marlonfangerrodrigues",
        bio: "Graduado em Redes de Computadores e Análise e Desenvolvimento de Sistemas pela FATEC Indaiatuba.",
        postGrad:
          "Pós-graduado em Segurança da Informação pela faculdade Líbano.",
      },
    ],
    // Services Section
    servicesTitle: "Nossos Principais Serviços",
    serviceDevTitle: "Desenvolvimento Personalizado",
    serviceDevText:
      "Construímos soluções digitais escaláveis e intuitivas, incluindo sites dinâmicos, progressive web apps (PWAs), sistemas de ponto de venda, sistemas de automação residencial (domótica) e aplicações de negócios personalizadas para suas necessidades operacionais específicas.",
    serviceInfraTitle: "Infraestrutura de TI",
    serviceInfraText:
      "Projetamos e gerenciamos ambientes de TI robustos. Nossos serviços incluem instalação de redes, integração de dispositivos de domótica, sistemas de controle de acesso seguro (biometria, facial), configuração de servidores e monitoramento contínuo para garantir o desempenho ideal.",
    serviceConsultTitle: "Consultoria Especializada",
    serviceConsultText:
      "Aproveite nossa experiência para tomar decisões tecnológicas informadas. Oferecemos orientação estratégica em desenvolvimento, infraestrutura e redes para alinhar sua estratégia de TI com seus objetivos de negócios para o sucesso a longo prazo.",
    // Portfolio Section
    portfolioTitle: "Nosso Portfólio",
    portfolio: [
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
    ],
    // Contact Section
    contactTitle: "Pronto para Elevar o Seu Negócio?",
    contactText:
      "Vamos conversar sobre como nossas soluções de TI podem ajudá-lo a alcançar seus objetivos. Entre em contato hoje para uma consulta.",
    contactButton: "Entre em Contato",
    // Footer
    footerRights: "© 2025 CDM Soluções em TI. Todos os Direitos Reservados.",
    // Contact Modal
    modalTitle: "Fale Conosco",
    modalText: "Preencha o formulário abaixo e retornaremos em breve.",
    modalName: "Nome Completo",
    modalEmail: "Email",
    modalPhone: "Telefone",
    modalMessage: "Descrição simples (Opcional)",
    modalSend: "Enviar Mensagem",
    // CTA Popup
    ctaPopupText: "Entre em contato",
  },
  en: {
    // Top Bar & Header
    followUs: "Follow us on social media",
    logoAlt: "CDM IT Logo",
    navAbout: "About",
    navFounders: "Founders",
    navServices: "Services",
    navProjects: "Projects",
    navContact: "Contact",
    // Hero Section
    heroTitle: "Building the Future of Your Business",
    heroSubtitle:
      "Custom Software, Robust Infrastructure, and Specialized IT Consulting",
    heroButton: "Explore Our Services",
    // About Section
    aboutTitle: "About CDM",
    aboutText:
      "Founded by <strong>Celso, Daniel, and Marlon</strong>, CDM IT Solutions is dedicated to empowering small and medium-sized businesses through technology. We believe in building strong partnerships, understanding your unique challenges, and delivering custom solutions that drive growth, efficiency, and innovation. Our combined experience is your asset in navigating the digital landscape.",
    // Founders Section (for Sobre.vue)
    foundersTitle: "Our Founders",
    owners: [
      {
        name: "Celso Rodrigo Giusti",
        role: "Infrastructure and Network Specialist",
        photoUrl: "celsoPhoto",
        linkedinUrl: "https://www.linkedin.com/in/celso-giusti-886b8596",
        bio: "Graduated in Systems Analysis and Development from FPM and Business Management from FATEC.",
      },
      {
        name: "Daniel Manoel Filho",
        role: "Software Development Specialist",
        photoUrl: "danielPhoto",
        linkedinUrl: "https://www.linkedin.com/in/dannmf",
        bio: "Graduated in Systems Analysis and Development from FATEC.",
      },
      {
        name: "Marlon Palata Fanger Rodrigues",
        role: "Information Security Specialist",
        photoUrl: "marlonPhoto",
        linkedinUrl: "https://www.linkedin.com/in/marlonfangerrodrigues",
        bio: "Graduated in Computer Networks and Systems Analysis and Development from FATEC Indaiatuba.",
        postGrad:
          "Post-graduate degree in Information Security from Líbano College.",
      },
    ],
    // Services Section
    servicesTitle: "Our Main Services",
    serviceDevTitle: "Custom Development",
    serviceDevText:
      "We build scalable and intuitive digital solutions, including dynamic websites, progressive web apps (PWAs), point-of-sale systems, home automation (domotics) systems, and custom business applications for your specific operational needs.",
    serviceInfraTitle: "IT Infrastructure",
    serviceInfraText:
      "We design and manage robust IT environments. Our services include network installation, home automation device integration, secure access control systems (biometric, facial), server configuration, and continuous monitoring to ensure optimal performance.",
    serviceConsultTitle: "Specialized Consulting",
    serviceConsultText:
      "Leverage our experience to make informed technology decisions. We offer strategic guidance in development, infrastructure, and networking to align your IT strategy with your business goals for long-term success.",
    // Portfolio Section
    portfolioTitle: "Our Portfolio",
    portfolio: [
      {
        client: "Sample Logistics Company",
        logo: "https://via.placeholder.com/150/2DA9B0/FFFFFF?text=Logo",
        description:
          "We developed a fleet management and real-time route optimization system, resulting in a 15% reduction in operational costs and a 20% increase in delivery efficiency.",
        link: "https://example.com",
        linkText: "View Case Study",
      },
      {
        client: "Sample Medical Clinic",
        logo: "https://via.placeholder.com/150/3E4A59/FFFFFF?text=Logo",
        description:
          "Implementation of an online scheduling system and electronic health record (PWA), improving the patient experience and centralizing information securely and accessibly for healthcare professionals.",
        link: null,
        linkText: "Internal System Project",
      },
    ],
    // Contact Section
    contactTitle: "Ready to Elevate Your Business?",
    contactText:
      "Let's talk about how our IT solutions can help you achieve your goals. Contact us today for a consultation.",
    contactButton: "Get in Touch",
    // Footer
    footerRights: "© 2025 CDM IT Solutions. All Rights Reserved.",
    // Contact Modal
    modalTitle: "Contact Us",
    modalText: "Fill out the form below and we will get back to you shortly.",
    modalName: "Full Name",
    modalEmail: "Email",
    modalPhone: "Phone",
    modalMessage: "Brief description (Optional)",
    modalSend: "Send Message",
    // CTA Popup
    ctaPopupText: "Contact Us",
  },
});
const t = computed(() => translations.value[language.value]);
provide("t", t);

function setLanguage(lang: "pt" | "en") {
  language.value = lang;
}

// --- OUTROS ESTADOS E FUNÇÕES ---
const isMenuOpen = ref(false);
const isContactFormOpen = ref(false);
const isScrolled = ref(false);
const isCtaPopupVisible = ref(false);
let ctaIntervalId: any = null; // CORREÇÃO: Mudei para 'any' para aceitar o tipo 'Timeout' do Node.

function showAndHidePopup() {
  isCtaPopupVisible.value = true;
  setTimeout(() => (isCtaPopupVisible.value = false), 10000);
}
function handleCtaInteraction() {
  isCtaPopupVisible.value = false;
}
function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value;
}
function closeMenu() {
  isMenuOpen.value = false;
}
function openContactForm() {
  isContactFormOpen.value = true;
}
function closeContactForm() {
  isContactFormOpen.value = false;
}
function handleScroll() {
  isScrolled.value = window.scrollY > 50;
}

const vFadeIn = {
  mounted: (el: HTMLElement) => {
    el.classList.add("fade-in");
    const observer = new IntersectionObserver(
      (entries) =>
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            el.classList.add("visible");
            observer.unobserve(el);
          }
        }),
      { threshold: 0.15 }
    );
    observer.observe(el);
  },
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  setTimeout(() => {
    showAndHidePopup();
    ctaIntervalId = setInterval(showAndHidePopup, 25000);
  }, 15000);
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
  if (ctaIntervalId) clearInterval(ctaIntervalId);
});
</script>

<template>
  <div id="top-bar">
    <div class="container">
      <div class="top-bar-left">
        <span class="social-follow-text">{{ t.followUs }}</span>
        <div class="social-media-bar">
          <a
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            title="LinkedIn"
          >
            <img
              src="https://cdn-icons-png.flaticon.com/512/174/174857.png"
              alt="LinkedIn"
            />
          </a>
          <a
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            title="Instagram"
          >
            <img
              src="https://cdn-icons-png.flaticon.com/512/2111/2111463.png"
              alt="Instagram"
            />
          </a>
          <a
            href="#"
            target="_blank"
            rel="noopener noreferrer"
            title="Facebook"
          >
            <img
              src="https://cdn-icons-png.flaticon.com/512/174/174848.png"
              alt="Facebook"
            />
          </a>
          <a href="#" target="_blank" rel="noopener noreferrer" title="TikTok">
            <img
              src="https://cdn-icons-png.flaticon.com/512/3046/3046121.png"
              alt="TikTok"
            />
          </a>
        </div>
      </div>
      <div class="controls-container">
        <button
          @click="setLanguage('pt')"
          class="control-button"
          title="Mudar para Português"
        >
          <img
            src="https://flagicons.lipis.dev/flags/4x3/br.svg"
            alt="Brasil Flag"
            class="flag-icon"
          />
        </button>
        <button
          @click="setLanguage('en')"
          class="control-button"
          title="Switch to English"
        >
          <img
            src="https://flagicons.lipis.dev/flags/4x3/gb.svg"
            alt="UK Flag"
            class="flag-icon"
          />
        </button>
        <button
          @click="toggleTheme"
          class="control-button theme-toggle"
          title="Mudar tema"
        >
          <span v-if="effectiveTheme === 'light'">🌙</span>
          <span v-if="effectiveTheme === 'dark'">☀️</span>
        </button>
      </div>
    </div>
  </div>
  <header id="header" :class="{ scrolled: isScrolled }">
    <nav class="container">
      <a href="#top-bar" class="logo-link" @click="closeMenu">
        <img
          :src="logoUrl"
          :alt="t.logoAlt"
          class="logo logo-dark-mode-adapt"
        />
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
        <li>
          <a href="#about" @click="closeMenu">{{ t.navAbout }}</a>
        </li>
        <li>
          <a href="#fundadores" @click="closeMenu">{{ t.navFounders }}</a>
        </li>
        <li>
          <a href="#services" @click="closeMenu">{{ t.navServices }}</a>
        </li>
        <li>
          <a href="#portfolio" @click="closeMenu">{{ t.navProjects }}</a>
        </li>
        <li>
          <a href="#contact" @click="closeMenu">{{ t.navContact }}</a>
        </li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="hero">
      <div class="hero-content container">
        <h1>{{ t.heroTitle }}</h1>
        <p class="subtitle">{{ t.heroSubtitle }}</p>
        <a href="#services" class="cta-button">{{ t.heroButton }}</a>
      </div>
    </section>

    <section id="about" v-fade-in>
      <div class="container">
        <h2>{{ t.aboutTitle }}</h2>
        <div class="about-logo-container">
          <img
            :src="logoUrl"
            :alt="t.logoAlt"
            class="about-logo logo-dark-mode-adapt"
          />
        </div>
        <p v-html="t.aboutText"></p>
      </div>
      <Sobre />
    </section>

    <section id="services" v-fade-in>
      <div class="container">
        <h2>{{ t.servicesTitle }}</h2>
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
            <h3>{{ t.serviceDevTitle }}</h3>
            <p>{{ t.serviceDevText }}</p>
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
            <h3>{{ t.serviceInfraTitle }}</h3>
            <p>{{ t.serviceInfraText }}</p>
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
            <h3>{{ t.serviceConsultTitle }}</h3>
            <p>{{ t.serviceConsultText }}</p>
          </div>
        </div>
      </div>
    </section>

    <section id="portfolio" v-fade-in>
      <div class="container">
        <h2>{{ t.portfolioTitle }}</h2>
        <div class="portfolio-list">
          <div
            v-for="project in t.portfolio"
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
        <h2>{{ t.contactTitle }}</h2>
        <p>{{ t.contactText }}</p>
        <button @click="openContactForm" class="cta-button">
          {{ t.contactButton }}
        </button>
      </div>
    </section>
  </main>

  <footer>
    <div class="container">
      <p>{{ t.footerRights }}</p>
    </div>
  </footer>

  <div
    v-if="isContactFormOpen"
    class="contact-form-overlay"
    @click.self="closeContactForm"
  >
    <div class="contact-form-modal">
      <button
        @click="closeContactForm"
        class="close-modal-btn"
        aria-label="Fechar formulário"
      >
        &times;
      </button>
      <h3>{{ t.modalTitle }}</h3>
      <p>{{ t.modalText }}</p>
      <form
        action="mailto:contato@cdmti.com.br"
        method="post"
        enctype="text/plain"
      >
        <div class="form-group">
          <label for="fullName">{{ t.modalName }}</label>
          <input type="text" id="fullName" name="Nome" required />
        </div>
        <div class="form-group">
          <label for="email">{{ t.modalEmail }}</label>
          <input type="email" id="email" name="Email" required />
        </div>
        <div class="form-group">
          <label for="phone">{{ t.modalPhone }}</label>
          <input type="tel" id="phone" name="Telefone" required />
        </div>
        <div class="form-group">
          <label for="message">{{ t.modalMessage }}</label>
          <textarea id="message" name="Mensagem" rows="4"></textarea>
        </div>
        <button type="submit" class="cta-button">{{ t.modalSend }}</button>
      </form>
    </div>
  </div>

  <transition name="cta-popup-fade">
    <div v-if="isCtaPopupVisible" class="cta-popup">
      <a href="#contact" @click="handleCtaInteraction" class="cta-popup-link">
        <span class="cta-popup-icon">💬</span>
        <span class="cta-popup-text">{{ t.ctaPopupText }}</span>
      </a>
      <button
        @click="handleCtaInteraction"
        class="cta-popup-close"
        aria-label="Fechar"
      >
        &times;
      </button>
    </div>
  </transition>
</template>

<style scoped>
#header {
  transition: box-shadow 0.3s ease-in-out;
}
#header.scrolled {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
</style>
