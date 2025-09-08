<div align="center">
  <h1>CDM Soluções em TI</h1>
  <p><strong>Construindo o Futuro do Seu Negócio com Tecnologia de Ponta.</strong></p>

  <p>
    <img alt="Vue.js" src="https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vue.js&logoColor=4FC08D" />
    <img alt="Vite" src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" />
    <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white" />
  </p>

  <p>
    <a href="#visão-geral">Visão Geral</a> •
    <a href="#recursos">Recursos</a> •
    <a href="#tecnologias-utilizadas">Tecnologias Utilizadas</a> •
    <a href="#como-executar-localmente">Como Executar </a> •
   <!-- <a href="#licença">Licença</a> -->
  </p>
</div>
 
## Visão Geral
 
Este é o repositório do site institucional da **CDM Soluções em TI**, uma landing page moderna e responsiva desenvolvida para apresentar a empresa, seus valores e portfólio de serviços.
 
O projeto foi construído com **Vue.js 3** e **Vite**, garantindo uma experiência de desenvolvimento ágil e um resultado final performático para o usuário.
 
<!--
##  Deploy

Acesse a versão ao vivo do projeto em: **[seusite.com.br](https://seusite.com.br)**
-->

## Recursos

- **Design Responsivo:** Interface totalmente adaptável para desktops, tablets e dispositivos móveis.
- **Animações Sutis:** Efeitos de fade-in ao rolar a página para uma experiência de usuário mais fluida e agradável.
- **Arquitetura Baseada em Componentes:** O projeto utiliza Single File Components (SFCs) do Vue para uma organização clara e modular.
- **Performance Otimizada:** Build rápido e eficiente graças ao Vite.

## Tecnologias Utilizadas

- **Vue.js 3:** Framework progressivo para construção de interfaces de usuário.
- **Vite:** Ferramenta de build moderna e rápida para desenvolvimento web.
- **TypeScript:** Superset do JavaScript que adiciona tipagem estática.

## Estrutura do Projeto

O projeto segue a estrutura padrão recomendada para aplicações Vue 3 com Vite, garantindo escalabilidade e manutenibilidade.

```
CDM/
├── node_modules/         # Dependências do projeto instaladas pelo npm/yarn
├── public/               # Arquivos estáticos que são copiados diretamente para a raiz do build
│   └── favicon.ico       # Exemplo: ícone do site
├── src/                  # Código-fonte da aplicação
│   ├── assets/           # Ativos estáticos (imagens, fontes, etc.) que são processados pelo bundler
│   │   ├── celso.png
│   │   ├── daniel.png
│   │   ├── logo_old.jpeg
│   │   ├── logo.png
│   │   └── marlon.png
│   ├── components/       # Componentes Vue reutilizáveis
│   │   └── Sobre.vue     # Exemplo: Componente para a seção "Sobre" ou "Equipe"
│   ├── App.vue           # Componente raiz da aplicação Vue
│   ├── index.css         # Estilos globais da aplicação
│   └── main.ts           # Ponto de entrada da aplicação TypeScript (monta o App.vue)
├── .env.local            # Variáveis de ambiente locais (não versionadas)
├── .gitignore            # Arquivos e diretórios a serem ignorados pelo Git
├── index.html            # Arquivo HTML principal (template para o SPA)
├── package-lock.json     # Garante versões exatas das dependências (gerado automaticamente)
├── package.json          # Metadados do projeto e scripts npm/yarn
├── README.md             # Este arquivo README
├── tsconfig.json         # Configurações do TypeScript para o código-fonte
├── tsconfig.node.json    # Configurações do TypeScript para arquivos Node.js (ex: vite.config.ts)
└── vite.config.ts        # Configuração do bundler Vite
```

> **Nota:** O arquivo principal da aplicação está nomeado como `index.tsx`, mas contém código Vue (Options API) e não JSX. O ponto de entrada em `index.html` aponta para `src/main.ts`. Certifique-se de que `main.ts` está importando e montando corretamente o componente definido em `index.tsx`.

## Como Executar Localmente

**Pré-requisitos:** Node.js instalado.

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/marlon-greg/CDM.git
   cd CDM
   ```

2. **Instale as dependências:**
   ```bash
   npm install
   ```
3. **Inicie o servidor de desenvolvimento:**
   ```bash
   npm run dev
   ```

Após executar o último comando, acesse o endereço local (geralmente `http://localhost:5173`) que aparecerá no seu terminal para visualizar o site.

<!--
## 📄 Licença

Este projeto não possui uma licença definida. Recomendo adicionar um arquivo `LICENSE` para esclarecer os termos de uso do código.
-->
