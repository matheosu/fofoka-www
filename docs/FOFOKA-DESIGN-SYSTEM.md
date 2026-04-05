# FOFOKA — Design System & Brand Reference
# Para uso como contexto do agente Claude no desenvolvimento do app

---

## 1. CONCEITO DO PRODUTO

Fofoka é uma rede social anônima baseada em geolocalização.
- Fofocas só podem ser vistas/postadas por quem está próximo do local marcado
- Anonimato total — sem perfil público, sem nome real
- Foco em diversão + segurança do usuário
- Sistema de reports robusto (assédio, fake, spam, discurso de ódio)
- Rankings de fofocas quentes por bairro/cidade/estado/país
- Conquistas gamificadas por engajamento positivo
- Tagline: "sussurra · localiza · some"

---

## 2. PALETA DE CORES

### Cores primárias da marca
```typescript
export const colors = {
  // === MARCA ===
  fogo:      '#E8593C',  // Cor primária, CTAs, logo, links, fab button
  brasa:     '#A33520',  // Hover/pressed states, pupilas do logo
  sussurro:  '#FFF7F0',  // Fundo claro, texto em dark mode
  segredo:   '#1A1A18',  // Fundo escuro (padrão do app), máscara do logo
  murmur:    '#B5A99A',  // Texto secundário, bordas, placeholders

  // === SEMÂNTICAS / FUNCIONAIS ===
  curtir:     '#45B26B',  // Like / thumbs up / sucesso
  report:     '#E85D50',  // Report / dislike / erro / perigo
  quente:     '#F5A623',  // Fofoca quente / destaque / warning
  rank:       '#6B7AE8',  // Rankings / posição / info
  conquista:  '#9B59B6',  // Conquistas / achievements / badges
  local:      '#3498DB',  // Localização / geo / mapa

  // === TEMPERATURA DOS PINS NO MAPA ===
  pinPegandoFogo: '#E8593C',  // Vermelho — olhos arregalados
  pinQuente:      '#F5A623',  // Laranja — olhos normais
  pinNormal:      '#B5A99A',  // Cinza — olhos relaxados
  pinFria:        '#6B7AE8',  // Azul — olhos semicerrados

  // === AUXILIARES ===
  cardBg:       'rgba(255, 247, 240, 0.035)',  // Fundo dos cards de fofoca
  cardBorder:   'rgba(255, 247, 240, 0.05)',   // Borda dos cards
  cardBgHot:    'rgba(245, 166, 35, 0.18)',    // Borda card "pegando fogo"
  textPrimary:  '#FFF7F0',                     // Texto principal (dark mode)
  textSecondary:'rgba(255, 247, 240, 0.45)',   // Texto secundário
  textMuted:    'rgba(255, 247, 240, 0.35)',   // Texto terciário, timestamps
  separator:    'rgba(255, 247, 240, 0.06)',   // Linhas divisórias
  tabBarBg:     'rgba(15, 15, 14, 0.97)',      // Fundo da tab bar
  overlay:      'rgba(15, 15, 14, 0.88)',      // Overlays, barra de busca no mapa
} as const;
```

### Cores de categoria de report
```typescript
export const reportCategories = {
  assedio:         { bg: 'rgba(232, 93, 80, 0.1)',  text: '#E85D50', label: 'Assédio' },
  fake:            { bg: 'rgba(245, 166, 35, 0.1)', text: '#F5A623', label: 'Fake' },
  spam:            { bg: 'rgba(181, 169, 154, 0.15)', text: '#B5A99A', label: 'Spam' },
  discursoDeOdio:  { bg: 'rgba(155, 89, 182, 0.1)', text: '#9B59B6', label: 'Discurso de ódio' },
} as const;
```

### Tags de temperatura (para badges e pills)
```typescript
export const temperatureTags = {
  pegandoFogo: { bg: 'rgba(245, 166, 35, 0.1)',  text: '#F5A623', label: 'pegando fogo' },
  quente:      { bg: 'rgba(232, 89, 60, 0.1)',    text: '#E8593C', label: 'quente' },
  normal:      { bg: 'rgba(181, 169, 154, 0.1)',   text: '#B5A99A', label: 'normal' },
  fria:        { bg: 'rgba(107, 122, 232, 0.1)',   text: '#6B7AE8', label: 'fria' },
} as const;
```

---

## 3. TIPOGRAFIA

### Fontes
```typescript
export const fonts = {
  heading:   'Poppins',      // Títulos, logo, headings — peso 700 (Bold) e 500 (Medium)
  body:      'DM Sans',      // Corpo de texto, fofocas, comentários — peso 400 (Regular)
  mono:      'JetBrains Mono', // Timestamps, distâncias, contadores, dados técnicos
} as const;
```

### Hierarquia de texto (StyleSheet)
```typescript
export const typography = StyleSheet.create({
  // Headings
  h1: { fontFamily: 'Poppins-Bold', fontSize: 24, color: '#E8593C' },
  h2: { fontFamily: 'Poppins-SemiBold', fontSize: 18, color: '#FFF7F0' },
  h3: { fontFamily: 'Poppins-Medium', fontSize: 15, color: '#FFF7F0' },

  // Body
  body: { fontFamily: 'DMSans-Regular', fontSize: 14, color: '#FFF7F0', lineHeight: 21 },
  bodySmall: { fontFamily: 'DMSans-Regular', fontSize: 12, color: '#FFF7F0' },

  // Caption / meta
  caption: { fontFamily: 'DMSans-Regular', fontSize: 11, color: 'rgba(255,247,240,0.45)' },
  mono: { fontFamily: 'JetBrainsMono-Regular', fontSize: 10, color: 'rgba(255,247,240,0.4)' },

  // Especiais
  logo: { fontFamily: 'Poppins-Bold', fontSize: 22, color: '#E8593C', letterSpacing: 1 },
  tag: { fontFamily: 'DMSans-Regular', fontSize: 10, color: '#E8593C' },
  badge: { fontFamily: 'DMSans-Regular', fontSize: 9, letterSpacing: 0.5 },
});
```

### Carregamento de fontes (Expo)
```typescript
import { useFonts } from 'expo-font';

const [fontsLoaded] = useFonts({
  'Poppins-Bold': require('./assets/fonts/Poppins-Bold.ttf'),
  'Poppins-SemiBold': require('./assets/fonts/Poppins-SemiBold.ttf'),
  'Poppins-Medium': require('./assets/fonts/Poppins-Medium.ttf'),
  'DMSans-Regular': require('./assets/fonts/DMSans-Regular.ttf'),
  'DMSans-Medium': require('./assets/fonts/DMSans-Medium.ttf'),
  'JetBrainsMono-Regular': require('./assets/fonts/JetBrainsMono-Regular.ttf'),
});
```

---

## 4. LOGO

### Conceito
O logo é um **pin de localização mascarado** (estilo Zorro):
- Pin laranja (#E8593C) = localização geográfica
- Máscara preta (#1A1A18) = anonimato
- Olhos com íris laranja = observação, curiosidade
- **Sem boca** = mistério, o observador silencioso
- A expressão vem APENAS dos olhos

### Variantes disponíveis (SVGs exportados)
- `logo-main.svg` — Logo principal, máscara preta (para fundo claro)
- `logo-darkmode.svg` — Máscara branca/creme (para fundo escuro)
- `logo-horizontal.svg` — Lockup horizontal: ícone + "fofoka" + tagline
- `logo-vertical.svg` — Lockup vertical: ícone em cima + "fofoka" embaixo
- `app-icon-512.svg` — Ícone do app (quadrado arredondado, só a máscara)
- `favicon.svg` — Favicon circular (só a máscara simplificada)

### Uso no app
- **Header do feed**: Texto "fofoka" em Poppins Bold 22px, cor #E8593C
- **Splash screen**: Logo vertical completo centralizado
- **Tab bar**: Não usa o logo, usa ícones de cada seção

---

## 5. PINS POR TEMPERATURA (MAPA)

Os pins no mapa mudam de aparência conforme a "temperatura" (popularidade) da fofoca.
A expressão é comunicada APENAS pela abertura dos olhos (sem boca).

| Temperatura    | Cor do pin | Olhos            | Quando usar                      |
|---------------|-----------|------------------|----------------------------------|
| Pegando fogo  | #E8593C   | Arregalados (rx=12, ry=9) | 500+ likes ou trending           |
| Quente        | #F5A623   | Normais (rx=10, ry=7)     | 100-499 likes                    |
| Normal        | #B5A99A   | Relaxados (rx=9, ry=6)    | 10-99 likes                      |
| Fria          | #6B7AE8   | Semicerrados (rx=9, ry=4) | < 10 likes                       |

### Tamanho dos pins no mapa
- Pegando fogo: 28x36px
- Quente: 24x32px
- Normal: 20x28px
- Fria: 18x24px

---

## 6. ESTRUTURA DE NAVEGAÇÃO (TABS)

```
app/
├── (tabs)/
│   ├── index.tsx          → Feed (lista de fofocas ao redor)
│   ├── mapa.tsx           → Visão de mapa com pins das fofocas
│   ├── ranking.tsx        → Rankings de fofocas quentes + top fofoqueiros
│   └── notificacoes.tsx   → Avisos (likes, comments, conquistas, reports)
├── (auth)/
│   ├── login.tsx
│   └── onboarding.tsx
├── perfil/
│   ├── index.tsx          → Perfil do usuário (anônimo)
│   ├── conquistas.tsx     → Lista completa de conquistas
│   └── configuracoes.tsx  → Configurações e privacidade
├── fofoca/
│   ├── [id].tsx           → Detalhe da fofoca + comentários
│   └── criar.tsx          → Criar nova fofoca (com emoji + local + hashtags)
└── _layout.tsx
```

### Tab bar
```typescript
const tabs = [
  { name: 'Feed',          icon: 'message-square',  route: '/(tabs)' },
  { name: 'Mapa',          icon: 'map-pin',         route: '/(tabs)/mapa' },
  { name: 'Rank',          icon: 'star',            route: '/(tabs)/ranking' },
  { name: 'Avisos',        icon: 'bell',            route: '/(tabs)/notificacoes', badge: true },
];
```

- Tab bar background: `rgba(15, 15, 14, 0.97)`
- Tab ativa: `#E8593C`
- Tab inativa: `rgba(255, 247, 240, 0.35)`
- Borda top: `1px solid rgba(255, 247, 240, 0.06)`
- FAB (Floating Action Button) para criar fofoca: círculo 52px, `#E8593C`, posição `bottom: 72, right: 16`

---

## 7. COMPONENTES PRINCIPAIS

### Card de fofoca (GossipCard)
```typescript
interface GossipCardProps {
  emoji: string;           // Emoji escolhido pelo criador (ex: 😱, 🤔, 👀)
  text: string;            // Texto da fofoca
  placeName: string;       // Nome do local do Google Maps (ex: "Café Floresta")
  timeAgo: string;         // Tempo relativo (ex: "5 min", "2h")
  temperature: 'pegandoFogo' | 'quente' | 'normal' | 'fria';
  hashtags: string[];      // Tags (ex: ["#casamento", "#constrangimento"])
  likes: number;
  dislikes: number;
  comments: number;
}
```

#### Estrutura visual do card:
1. **Meta row**: Badge de temperatura + ícone pin + nome do local + tempo
2. **Texto da fofoca**: DM Sans 13.5px, cor #FFF7F0, lineHeight 1.5
3. **Hashtags**: Pills com fundo `rgba(232,89,60,0.1)`, texto #E8593C, fontSize 10
4. **Emoji row**: Emoji escolhido pelo criador como thumbnail/avatar do post
5. **Action bar**: Like, dislike, comentar, compartilhar

#### Estilos do card:
```typescript
const gossipCard = StyleSheet.create({
  container: {
    marginHorizontal: 12,
    marginVertical: 5,
    padding: 14,
    backgroundColor: 'rgba(255, 247, 240, 0.035)',
    borderRadius: 16,
    borderWidth: 1,
    borderColor: 'rgba(255, 247, 240, 0.05)',
  },
  containerHot: {
    borderColor: 'rgba(245, 166, 35, 0.18)',
  },
});
```

### Emoji como ícone da fofoca
- Na criação, o usuário escolhe 1 emoji que representa a fofoca
- Esse emoji vira o avatar/thumbnail do post
- Exibido dentro de um quadrado arredondado (44x44, borderRadius 12) com fundo colorido sutil
- Cor do fundo do emoji: `rgba(corDaTemperatura, 0.15)`

### Hashtags
- Pills com borderRadius 10
- Background: `rgba(232, 89, 60, 0.1)`
- Texto: #E8593C, fontSize 10, fontFamily DM Sans
- Precedidas por # automaticamente

### Sistema de report
Categorias com pills coloridos:
- Assédio: vermelho (#E85D50)
- Fake: laranja (#F5A623)  
- Spam: cinza (#B5A99A)
- Discurso de ódio: roxo (#9B59B6)

---

## 8. NOTIFICAÇÕES (TELA AVISOS)

Tipos de notificação e seus ícones/cores:
```typescript
const notificationTypes = {
  fogoAlert:    { icon: 'flame',        bg: 'rgba(245,166,35,0.12)',  color: '#F5A623' },
  like:         { icon: 'thumbs-up',    bg: 'rgba(69,178,107,0.12)',  color: '#45B26B' },
  comment:      { icon: 'message',      bg: 'rgba(232,89,60,0.12)',   color: '#E8593C' },
  conquista:    { icon: 'trophy',       bg: 'rgba(155,89,182,0.12)',  color: '#9B59B6' },
  rankUp:       { icon: 'star',         bg: 'rgba(107,122,232,0.12)', color: '#6B7AE8' },
  reportResult: { icon: 'shield',       bg: 'rgba(232,93,80,0.12)',   color: '#E85D50' },
  nearbyNew:    { icon: 'map-pin',      bg: 'rgba(52,152,219,0.12)', color: '#3498DB' },
};
```

- Notificações não lidas: fundo `rgba(232, 89, 60, 0.04)`
- Ícone: círculo 36px com background colorido sutil
- Texto: DM Sans 12px, nomes de locais em **bold cor #E8593C**
- Timestamp: JetBrains Mono 10px, cor `rgba(255,247,240,0.35)`

---

## 9. CONQUISTAS (DENTRO DO PERFIL)

As conquistas ficam acessíveis via menu no perfil, não na tab bar.
São desbloqueadas e notificadas na tela de Avisos.

### Categorias de conquistas:
```typescript
const achievements = [
  // Por fofocas feitas
  { id: 'isqueiro',      name: 'Isqueiro',           desc: '10 fofocas quentes',       icon: 'flame',     color: '#F5A623' },
  { id: 'incendiario',   name: 'Incendiário',        desc: '50 fofocas quentes',       icon: 'flame',     color: '#E8593C' },

  // Por visualizações
  { id: 'espiao',         name: 'Espião',             desc: '100 fofocas vistas',       icon: 'eye',       color: '#B5A99A' },

  // Por curtidas recebidas
  { id: 'queridinho',     name: 'Queridinho',         desc: '500 curtidas recebidas',   icon: 'heart',     color: '#45B26B' },

  // Por comentários
  { id: 'engajador',      name: 'Engajador',          desc: '100 comentários',          icon: 'message',   color: '#E8593C' },

  // Por reports corretos
  { id: 'guardiao',       name: 'Guardião',           desc: '20 reports corretos',      icon: 'shield',    color: '#E85D50' },

  // Por geografia
  { id: 'turista',        name: 'Turista',            desc: 'Fofocou em 5 cidades',     icon: 'map',       color: '#3498DB' },
  { id: 'fofLocalBairro', name: 'Fofoqueiro local',   desc: '50 fofocas no bairro',     icon: 'map-pin',   color: '#9B59B6' },
  { id: 'fofEstadual',    name: 'Fofoqueiro estadual', desc: 'Ativo em 3+ cidades do estado', icon: 'map', color: '#6B7AE8' },
  { id: 'fofNacional',    name: 'Fofoqueiro nacional', desc: 'Ativo em 5+ estados',     icon: 'globe',     color: '#E8593C' },

  // Por ranking
  { id: 'lenda',          name: 'Lenda',              desc: 'Top 1 da cidade',          icon: 'crown',     color: '#F5A623' },
  { id: 'mestre',         name: 'Mestre',             desc: 'Top 3 da cidade',          icon: 'award',     color: '#6B7AE8' },
];
```

### Card de conquista:
- Grid 2 colunas
- Background: `rgba(cor, 0.08)`
- Ícone: 28px, cor da conquista
- Nome: Poppins SemiBold 11px, cor da conquista
- Descrição: DM Sans 9px, opacity 0.6
- Barra de progresso: height 3px, borderRadius 2px, fundo `rgba(0,0,0,0.15)`

---

## 10. MAPA

### Visão geral
- Fundo escuro (#1A1A18) com ruas em `rgba(255,247,240,0.08)`
- Blocos/quadras em `rgba(255,247,240,0.03)` com borderRadius 4
- Pins das fofocas com tamanho proporcional à popularidade
- Hover/tap no pin mostra tooltip com nome do local + likes + temperatura

### Controles do mapa
- Barra de busca: height 36, borderRadius 18, fundo `rgba(15,15,14,0.88)`
- Filtro: pill com ícone, mesmo estilo da busca
- Legenda: pills na base com dot colorido + label da temperatura

---

## 11. RANKING

### Seções do ranking:
1. **Fofocas mais quentes** (do bairro/cidade) — ícone chama #F5A623
2. **Top fofoqueiros** (da cidade/estado) — ícone pessoa #9B59B6

### Item do ranking:
- Número da posição: Poppins Bold 17px
  - #1: cor #F5A623 (ouro)
  - #2: cor #B5A99A (prata)
  - #3: cor #A33520 (bronze)
- Nome: DM Sans 12.5px, #FFF7F0
- Score: JetBrains Mono 9.5px, rgba(255,247,240,0.4)
- Badge opcional: pill com label (ex: "lenda", "mestre", "fogo")

---

## 12. REGRAS GERAIS DE DESIGN

### Dark mode é o padrão
O app inteiro usa fundo escuro (#0F0F0E ou #1A1A18). Isso combina com a vibe de segredo/anonimato.

### Bordas e separadores
- Sempre ultrafinos: 0.5-1px
- Cor: `rgba(255, 247, 240, 0.06)` para separadores
- BorderRadius: 16px para cards, 12px para pills/tags, 18px para inputs

### Ícones
- Usar Lucide React Native ou similar (outline style, stroke-width 2)
- Tamanho padrão: 20px na tab bar, 14px nas actions, 12px nos meta

### Animações
- Usar react-native-reanimated
- Press in: scale(0.95) com spring
- Cards: fade in staggered no feed
- FAB: scale bounce ao aparecer
- Tab switch: crossfade

### Espaçamento
- Padding horizontal do feed: 12px
- Gap entre cards: 5-6px vertical
- Padding interno dos cards: 14px
- Gap entre action buttons: 14-16px

---

## 13. ASSETS SVG DISPONÍVEIS

Todos os SVGs estão na pasta do projeto e são vetoriais (escaláveis para qualquer resolução).

```
assets/brand/
├── logos/
│   ├── logo-main.svg          # Pin mascarado, máscara preta
│   ├── logo-darkmode.svg      # Pin mascarado, máscara branca
│   ├── logo-horizontal.svg    # Ícone + wordmark horizontal
│   └── logo-vertical.svg      # Ícone + wordmark vertical
├── icons/
│   ├── app-icon-512.svg       # Ícone do app (quadrado arredondado)
│   └── favicon.svg            # Favicon circular
└── pins/
    ├── pin-pegando-fogo.svg   # Vermelho, olhos arregalados
    ├── pin-quente.svg         # Laranja, olhos normais
    ├── pin-normal.svg         # Cinza, olhos relaxados
    └── pin-fria.svg           # Azul, olhos semicerrados
```

---

## INSTRUÇÕES PARA O AGENTE

Ao aplicar este design system no app Fofoka (React Native/Expo):

1. **Substituir todas as cores existentes** pelos valores definidos na seção 2
2. **Carregar as fontes** Poppins, DM Sans e JetBrains Mono via expo-font
3. **Aplicar a hierarquia tipográfica** da seção 3 em todos os textos
4. **Usar o logo** conforme a seção 4 — texto "fofoka" em Poppins Bold no header
5. **Implementar os cards de fofoca** com a estrutura da seção 7 (emoji + local do Google Maps + hashtags + temperatura)
6. **Tab bar** com 4 tabs: Feed, Mapa, Rank, Avisos (conquistas ficam no perfil)
7. **Dark mode como padrão** — fundo #0F0F0E, todo texto claro
8. **Manter consistência** nos border-radius, espaçamentos e cores semânticas
9. **Copiar os SVGs** para assets/brand/ e usar como referência para ícones customizados
