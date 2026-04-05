# FOFOKA.COM — Landing Page & Site Spec
# Para implementação via Claude Code + deploy no Cloudflare Pages

---

## 1. VISÃO GERAL

Site institucional do Fofoka — rede social anônima por geolocalização.
Objetivo: apresentar o produto, gerar downloads (App Store + Google Play), transmitir confiança e segurança.

### Stack
- Astro (SSG) para i18n nativo + componentes + static export
- Alternativa: HTML/CSS/JS puros com pastas por idioma
- Deploy: Cloudflare Pages

### Estrutura de arquivos
```
fofoka-site/
├── src/
│   ├── pages/
│   │   ├── pt/                      # Português (padrão)
│   │   │   ├── index.astro
│   │   │   ├── privacidade.astro
│   │   │   ├── termos.astro
│   │   │   ├── ajuda.astro
│   │   │   ├── contato.astro
│   │   │   └── diretrizes.astro
│   │   ├── en/                      # English
│   │   │   ├── index.astro
│   │   │   ├── privacy.astro
│   │   │   ├── terms.astro
│   │   │   ├── help.astro
│   │   │   ├── contact.astro
│   │   │   └── guidelines.astro
│   │   └── index.astro              # Detect locale → /pt/ ou /en/
│   ├── components/
│   │   ├── Navbar.astro
│   │   ├── Footer.astro
│   │   ├── Hero.astro
│   │   ├── FeatureCard.astro
│   │   ├── SecuritySection.astro
│   │   ├── RankingSection.astro
│   │   ├── CTASection.astro
│   │   ├── FAQ.astro
│   │   ├── ContactForm.astro
│   │   ├── LanguageSwitcher.astro
│   │   ├── StoreButton.astro
│   │   └── PinMascot.astro
│   ├── i18n/
│   │   ├── pt.json
│   │   └── en.json
│   └── layouts/
│       └── Base.astro
├── public/
│   ├── assets/ (logos/, icons/, pins/)
│   ├── _redirects
│   └── _headers
└── CLAUDE.md
```

---

## 2. i18n — INTERNACIONALIZAÇÃO

### Idiomas: pt (padrão) + en

### Detecção de idioma (index raiz)
```javascript
const lang = navigator.language.startsWith('pt') ? 'pt' : 'en';
window.location.replace('/' + lang + '/');
```

### Language switcher
- Navbar, à direita, antes do CTA
- Pill: "🇧🇷 PT" / "🇺🇸 EN", fontSize 12, border 1px solid var(--border), borderRadius 20px
- Mapeamento: /pt/ajuda ↔ /en/help, /pt/privacidade ↔ /en/privacy, etc.

### hreflang (todas as páginas)
```html
<link rel="alternate" hreflang="pt" href="https://fofoka.com/pt/">
<link rel="alternate" hreflang="en" href="https://fofoka.com/en/">
<link rel="alternate" hreflang="x-default" href="https://fofoka.com/pt/">
```

### Tagline por idioma
- PT: "sussurra · localiza · some"
- EN: "whisper · locate · vanish"

### Textos i18n — pt.json (resumo das chaves)
- nav: features, security, help, download, contact
- hero: title_1/2/3, subtitle, tagline, app_store, google_play
- how_it_works: title, location(title+desc), anonymous(title+desc), ephemeral(title+desc)
- features: title, temperature(title+desc+levels), comments, likes, hashtags, emoji, map
- ranking: title, subtitle, rankings(title+items[]), achievements(title+items[]), scale
- security: title_1/2, subtitle, reports{harassment,fake,spam,hate}(title+desc), ai, encryption, report, privacy_link
- cta: title_1/2, counter
- footer: product, legal, contact, features, security, help, privacy, terms, guidelines, copyright
- help: title, search_placeholder, categories{}, faq[{q,a,cat}]
- contact: title, subtitle, form{name,email,subject,subjects[],message,submit,success,placeholders}
- privacy/terms/guidelines: title, last_updated

### Textos i18n — en.json
- Mesma estrutura, traduzido. Hero: "Discover what's happening / around you. / Anonymously."
- Security: "Anonymous, but / safe."
- FAQ com 10 perguntas traduzidas

O agente deve criar os JSONs completos com todos os textos necessários.

---

## 3. IDENTIDADE VISUAL

### Cores CSS
```css
:root {
  --fogo: #E8593C; --brasa: #A33520; --sussurro: #FFF7F0;
  --segredo: #1A1A18; --murmur: #B5A99A;
  --curtir: #45B26B; --report: #E85D50; --quente: #F5A623;
  --rank: #6B7AE8; --conquista: #9B59B6; --local: #3498DB;
  --bg: #0F0F0E; --bg-card: rgba(255,247,240,0.035);
  --bg-elevated: #1A1A18; --bg-footer: #0A0A09;
  --text: #FFF7F0; --text-2: rgba(255,247,240,0.55);
  --text-3: rgba(255,247,240,0.35); --border: rgba(255,247,240,0.06);
}
```

### Tipografia
```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&family=DM+Sans:wght@400;500&family=JetBrains+Mono:wght@400&display=swap');
--font-heading: 'Poppins', sans-serif;
--font-body: 'DM Sans', sans-serif;
--font-mono: 'JetBrains Mono', monospace;
```

### Logo
- Pin mascarado (Zorro), sem boca, olhos olhando pra direita
- Landing (fundo escuro): usar logo-darkmode.svg (máscara branca)
- Navbar: ícone 28px + "fofoka" Poppins Bold 20px, Fogo
- Favicon: favicon.svg

---

## 4. LANDING PAGE — SEÇÕES

### NAVBAR (sticky)
- Height 64px, bg rgba(15,15,14,0.85), backdrop-filter blur(12px), z-index 100
- Logo: ícone + "fofoka" à esquerda
- Links desktop: Recursos, Segurança, Ajuda — DM Sans 14px, var(--text-2)
- Language switcher: pill com bandeira
- CTA: "Baixar app", bg Fogo, color Sussurro, borderRadius 24px
- Mobile: logo + lang + hamburger

### HERO
- Pin mascarado 120px com animação float (translateY -8px↔0, 3s loop)
- Título: Poppins Bold 48px/32px mobile, "Anonimamente." em Fogo
- Subtítulo: DM Sans 18px/15px, var(--text-2), maxWidth 480px
- Botões: App Store (fundo branco) + Google Play (fundo branco), height 52, borderRadius 14
- Tagline: 12px, Murmúrio, letterSpacing 5px

### COMO FUNCIONA (3 cards)
- Título: Poppins Bold 36px/28px, center
- Grid 3col/1col mobile, gap 24px, maxWidth 960px
- Cards: bg var(--bg-card), borderRadius 20px, border, padding 32px
- 3 cards: Localização (pin azul), Anônimo (máscara vermelha), Efêmero (pin cinza)

### RECURSOS (6 features zigzag)
- Título: Poppins Bold 36px, center
- Layout zigzag desktop (imagem alterna esquerda/direita), stack mobile
- Features: Temperatura (com 4 pins SVG em fila), Comentários, Likes, Hashtags, Emoji, Mapa
- Título feature: Poppins SemiBold 22px
- Desc: DM Sans 16px, var(--text-2)

### RANKING & CONQUISTAS (2 cards)
- Grid 2col/1col, gap 24px
- Rankings: lista com bullets cor Quente
- Conquistas: lista com bullets cor Conquista
- "bairro → cidade → estado → país!" com setas Fogo

### SEGURANÇA (seção crítica)
- Título: "Anônimo, mas seguro." — "seguro" em Curtir (#45B26B)
- Grid 4 reports: Assédio (#E85D50), Fake (#F5A623), Spam (#B5A99A), Discurso de ódio (#9B59B6)
- Cada card: bg rgba(cor,0.08), borderRadius 16px, border 1px solid rgba(cor,0.15)
- 3 items: IA 24h, Dados criptografados, Report instantâneo
- Link para política de privacidade em Fogo

### CTA FINAL
- bg var(--bg-elevated), pin 80px, título, botões store, tagline

### FOOTER
- bg #0A0A09
- Grid 3col/1col: Produto, Legal, Contato
- Copyright com tagline

---

## 5. PÁGINAS AUXILIARES

Todas: navbar + conteúdo (maxWidth 720px, padding 48px 24px) + footer.

### Privacidade / Privacy
- Poppins Bold 36px, data atualização, corpo DM Sans 16px lineHeight 1.8
- Seções: Coleta, Uso, Anonimato, Armazenamento, Compartilhamento, Direitos, Cookies, DPO

### Termos / Terms
- Seções: Aceitação, Uso, Conteúdo proibido, Reports, Propriedade intelectual, Limitações, Alterações

### Ajuda / Help
- Busca (input + lupa, filtra em tempo real)
- Tabs/filtro por categoria (5 categorias)
- Accordion: pergunta Poppins SemiBold 16px + resposta DM Sans 15px
- Chevron rotaciona ao expandir
- 10 FAQs por idioma (definidas no i18n JSON)

### Contato / Contact
- Formulário: Nome, Email, Assunto (select com 5 opções), Mensagem (textarea)
- Inputs: height 48px, borderRadius 12px, bg var(--bg-card), focus border Fogo
- Botão: bg Fogo, height 48px, borderRadius 14px
- Email direto: contato@fofoka.com
- Nota: "Respondemos em até 48h"

### Diretrizes / Guidelines
- Seções: Permitido, Proibido, Reports, Consequências, Apelação

---

## 6. RESPONSIVIDADE

```css
/* Mobile first */
@media (min-width: 640px) { /* Tablet */ }
@media (min-width: 1024px) { /* Desktop */ }
```
- Títulos: 28-32px mobile → 36-48px desktop
- Grids: 1col → 2-3col
- Navbar: hamburger → links inline
- Padding seções: 48px 16px → 96px 24px
- Max-width: 1200px

---

## 7. ANIMAÇÕES

- Scroll reveal: IntersectionObserver, fade-in + translateY(30px→0), 600ms ease-out
- Stagger grids: delay 100ms * index
- Pin hero: float (translateY -8px↔0, 3s ease-in-out infinite)
- Navbar: transparente → blur on scroll
- FAQ: max-height transition 300ms
- Botões: scale(0.98) on active

---

## 8. CLOUDFLARE CONFIG

### _redirects
```
/ /pt/ 302
https://www.fofoka.com/* https://fofoka.com/:splat 301
```

### _headers
```
/*
  X-Content-Type-Options: nosniff
  X-Frame-Options: DENY
  Referrer-Policy: strict-origin-when-cross-origin

/assets/*
  Cache-Control: public, max-age=31536000, immutable
```

---

## 9. ASSETS

### Existentes (copiar de assets/brand/):
- logos/: logo-main.svg, logo-darkmode.svg, logo-horizontal.svg, logo-vertical.svg
- icons/: favicon.svg, app-icon-512.svg
- pins/: pin-pegando-fogo.svg, pin-quente.svg, pin-normal.svg, pin-fria.svg

### Criar:
- icons/apple-touch-icon.png (180x180, do app-icon)
- og-image.png (1200x630, fundo escuro + logo + tagline)
- Store badges SVG (App Store + Google Play)

---

## 10. SEO

- Meta tags: title, description, og:*, twitter:*
- hreflang em todas as páginas
- sitemap.xml gerado automaticamente
- robots.txt com sitemap reference
- Structured data (JSON-LD): Organization + SoftwareApplication

---

## 11. INSTRUÇÕES PARA O AGENTE

1. Ler este spec ANTES de implementar
2. Criar os JSONs de i18n COMPLETOS com todos os textos (pt.json + en.json)
3. Copiar SVGs de assets/brand/ para public/assets/
4. Landing é sempre dark mode (sem toggle)
5. Todas as páginas: navbar com language switcher + footer
6. FAQ: accordion com busca funcional usando dados do i18n
7. Formulário de contato: frontend only (placeholder no submit)
8. Testar responsividade: 320px, 640px, 1024px, 1440px
9. Gerar sitemap.xml + robots.txt
10. Garantir hreflang correto em todas as páginas
