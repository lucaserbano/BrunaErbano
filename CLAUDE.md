# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Website for cardiologist Bruna Erbano. Built with **Next.js (App Router) + Tailwind CSS**, entirely in **Brazilian Portuguese**. Features a scroll-driven video experience in the hero section.

## Commands

```bash
npm run dev      # Start development server
npm run build    # Production build
npm run start    # Start production server
npm run lint     # Run ESLint
```

## Architecture

### Stack
- **Next.js App Router** — pages live in `app/`, layouts in `app/layout.tsx`
- **Tailwind CSS** — brand colors, fonts, and spacing extended in `tailwind.config.ts`
- **GSAP ScrollTrigger** (or native scroll events) — powers scroll-driven video in Hero

### Page Structure
Single-page layout with anchor-linked sections:
- `Hero` — scroll-synchronized video (see below)
- `Sobre` — bio and background
- `Serviços` — cardiology services/procedures
- `Galeria` — photo/media gallery
- `FAQ` — frequently asked questions
- `Contato` — appointment booking / contact form

Components live in `src/components/`, one file per section.

### Scroll-Driven Video (Hero)
The hero video scrubs based on scroll position. Pattern:

```tsx
const videoRef = useRef<HTMLVideoElement>(null);

useEffect(() => {
  // GSAP ScrollTrigger approach
  ScrollTrigger.create({
    trigger: heroRef.current,
    start: "top top",
    end: "bottom bottom",
    scrub: true,
    onUpdate: (self) => {
      if (videoRef.current) {
        videoRef.current.currentTime =
          self.progress * videoRef.current.duration;
      }
    },
  });
}, []);
```

The video must be preloaded (`preload="auto"`) and muted. The hero section needs enough scroll height (e.g., `height: 300vh`) to give the effect room.

### Assets
Media files (images, videos) are stored in a **custom root-level folder** (e.g., `/assets/` or `/media/`), not in `public/`. To serve them in Next.js, either:
- Copy/move to `public/` at build time via a script in `package.json`
- Or configure a custom Next.js route in `next.config.ts`

### Branding
Brand tokens (colors, typography) are configured in `tailwind.config.ts` under `theme.extend`. Do not use hardcoded color values in components — always use Tailwind brand tokens.

### Language
All user-facing text is in PT-BR. No i18n library is used. Text content is colocated in each component or in a `src/content/` data file.

---

## Identidade Visual

### Tipografia
- Fonte única: **Raleway** (importar do Google Fonts — weights 300 e 500)
- Corpo/texto corrido: `font-weight: 300` (Raleway Light)
- Títulos e botões: `font-weight: 500` (Raleway Medium)
- Não usar Roboto como fonte principal

### Paleta de cores (com regras de uso — fonte: Manual de Identidade Visual)

| Token Tailwind  | HEX       | Uso                                                              |
|-----------------|-----------|------------------------------------------------------------------|
| `brand-blue`    | `#2C65D0` | 40–50% — botões, destaques, gradientes, fundos                   |
| `brand-dark`    | `#0D1220` | 30–40% — textos principais, contornos, fundos escuros            |
| `brand-light`   | `#F5F9FD` | 20–30% — fundo principal, navbar, rodapé, texto em fundo colorido|
| `brand-gray`    | `#86959B` | 10–20% — detalhes, bordas, contraste com azul escuro             |
| `brand-black`   | `#000000` | secundário                                                       |
| `brand-white`   | `#FFFFFF` | secundário                                                       |

### Gradiente principal
`linear-gradient(-45deg, #2C65D0, #0D1220)` — usar em hero, seções de destaque e CTAs com fundo escuro.

### Símbolo da marca
O símbolo é um traçado estilizado de ECG (eletrocardiograma) — linhas horizontais que remetem ao monitor cardíaco. Pode ser usado como elemento decorativo em separadores, ícones e backgrounds.
Arquivos locais: `assets/arquivos identidade visual/`

### Padrões decorativos
O manual inclui dois padrões de fundo (texturas com linhas diagonais repetidas):
- Padrão denso azul (linhas azuis sobre branco) — para seções de destaque
- Padrão suave claro (linhas finas sobre branco) — para seções secundárias

### Variantes do logo
- Horizontal: `assets/arquivos identidade visual/` (também em: https://brunaerbano.com.br/wp-content/uploads/2025/07/Prancheta-26.png)
- Vertical: `assets/arquivos identidade visual/`
- Símbolo isolado: `assets/arquivos identidade visual/`
- Tagline: "CARDIOLOGISTA e ECOCARDIOGRAFISTA"

---

## Conteúdo das seções

### Hero (Início)
- Headline: "Cardiologia com precisão. Ecocardiografia com excelência."
- Subtítulo: "Medicina moderna guiada por imagem em Curitiba-PR."
- CTA primário: "Agende seu exame!" → `https://wa.me/5541996958826?text=Olá!%20Gostaria%20de%20agendar%20meu%20exame%20com%20a%20Dra.%20Bruna%20Erbano.`

### Serviços (6 cards)
1. **Ecocardiograma Transtorácico** — Exame de imagem não invasivo que usa ultrassom para avaliar a estrutura e o funcionamento do coração em tempo real.
2. **Ecocardiograma Transesofágico** — Exame de imagem que utiliza ultrassom por uma sonda no esôfago para avaliar o coração com maior detalhamento e precisão.
3. **Ecocardiograma Tridimensional (3D)** — Exame de imagem que utiliza ultrassom tridimensional para avaliar o coração em tempo real, com maior precisão anatômica e funcional.
4. **Ecocardiograma Strain** — Avalia a deformação do músculo cardíaco, permitindo detectar alterações sutis da função do coração antes que se tornem aparentes.
5. **Ecocardiograma Intra-operatório** — Exame realizado durante cirurgias cardíacas ou procedimentos transcateter.
6. **Doppler de Carótidas e Vertebrais** — Exame de ultrassom que avalia o fluxo sanguíneo e possíveis obstruções nas artérias que irrigam o cérebro.

### Sobre
- **Missão:** Diagnóstico de cardiopatias com acurácia baseada em evidências atuais, visando o tratamento adequado e o cuidado de cada paciente. Referência em Cardiologia (Valvulopatias) e Ecocardiografia, unindo excelência técnica, empatia e atendimento personalizado.
- **Valores:** Excelência, ética, empatia, precisão diagnóstica e compromisso com o paciente.
- **Formação:**
  - Cardiologista — Instituto Dante Pazzanese de Cardiologia (SP), certificada pela SBC (2º lugar nacional, 2020)
  - Ecocardiografista — Instituto do Coração (InCor/FMUSP), certificada pelo DIC/SBC
  - Mestra em Medicina Cardiovascular — USP
- **Atuação clínica:** Hospital de Clínicas (UFPR), Hospital Cajuru, Hospital São Marcelino Champagnat, Instituto de Neurologia de Curitiba (INC - Ecoville), Quanta Diagnóstico por Imagem
- **Acadêmica:** Professora de pós-graduação em Ecocardiografia (Afya), co-editora da plataforma The Valve Club, autora/co-autora de 20+ artigos publicados em revistas científicas e 60+ trabalhos apresentados em congressos.

### Contato
- **WhatsApp:** +55 41 99695-8826
- **Instagram:** @bruna.erbano
- **CTA:** "Fale comigo!" → `https://wa.me/5541996958826`

**Locais de atendimento:**
1. **Quanta Diagnóstico por Imagem** — Av. Sete de Setembro 4751, Batel, Curitiba/PR | Hospital: (41) 3281-5555 | Cardio: (41) 3281-5501
2. **Hospital Cajuru** — Av. Getúlio Vargas 1625, Seminário, Curitiba/PR | (41) 3310-7500
3. **Hospital de Clínicas (UFPR)** — R. General Carneiro 181, Centro, Curitiba/PR | (41) 3360-1800
4. **Instituto de Neurologia de Curitiba – Ecoville** — R. Jeremias Maciel Perretto 300, Ecoville, Curitiba/PR | INC: (41) 3028-8545 | Cardio: (41) 3028-8551
5. **Hospital São Marcelino Champagnat** — Av. Presidente Affonso Camargo 1399, Cristo Rei, Curitiba/PR | (41) 3087-7600

---

## SEO / Metadata padrão

- **Title:** "Bruna Erbano - Cardiologista e Ecocardiografista"
- **Description:** "Médica que atua em Curitiba-PR realizando exames como o Ecocardiograma ambulatorial (2D, 3D e Strain), intraprocedimento, intra-operatório, além de Doppler de Carótidas e Vertebrais."
- **og:locale:** `pt_BR`
- **robots:** `index, follow, max-snippet:-1, max-image-preview:large, max-video-preview:-1`
- **Favicon (32px):** `https://brunaerbano.com.br/wp-content/uploads/2026/01/cropped-logo-para-icone-pagina-32x32.jpg`
- **og:image (270px):** `https://brunaerbano.com.br/wp-content/uploads/2026/01/cropped-logo-para-icone-pagina-270x270.jpg`
- **Site URL:** `https://brunaerbano.com.br/`
