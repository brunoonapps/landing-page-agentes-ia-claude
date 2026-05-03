# CLAUDE.md — Landing Page "Agentes IA com Claude Agent SDK + MCP"

> Briefing para o agente de manutenção desta landing.
> Leia isto na íntegra antes de propor qualquer mudança.

## 1. Contexto do produto

**O que é:** página de vendas de um infoproduto técnico premium em PT-BR sobre Claude Agent SDK + MCP.

- **Autor:** Bruno Santos · `linkedin.com/in/brunoonapps`
- **Plataforma de venda:** Hotmart (produto ID `7661508`)
- **Tíquete:** R$ 397 (oferta principal "Lançamento") · R$ 277,90 com cupom `EARLYBIRD30` (primeiros 7 dias)
- **Público-alvo:** devs intermediário/avançado em TS/Python/Go/Rust, founders técnicos, criadores de conteúdo dev
- **Bundle entregue:** ebook 237 págs + 4 PDFs de bônus + comunidade exclusiva + **Lab Docker production-grade (Bônus 5)** validado em runtime real contra a API Anthropic
- **Posicionamento:** o livro técnico que começa onde os "tutoriais de prompt" terminam — todos os 7 projetos validados em runtime real, não só "static analysis"

### Histórico de mudanças relevantes (changelog do briefing)

- **2026-05-02:** validação runtime concluída pelo Claude Code. 3 bugs corrigidos (modelos descontinuados, tipos do agentic loop, mock do projeto 06). Adicionado Bônus 5 — Lab Docker production-grade com docker-compose, Postgres seedado, MCP servers validados via Inspector, 25 testes automatizados passando, custo total da validação ~US$ 0,08. Headline da seção bônus saiu de "R$ 500" para "R$ 800 em bônus". Pill "10+ skills profissionais" virou "Lab Docker validado" no hero. Meta description atualizada com runtime validation.

## 2. Stack & filosofia técnica

A landing é **deliberadamente simples**:

- HTML único standalone (`index.html`) — sem build, sem framework, sem bundler
- Fontes via Google Fonts (Inter + JetBrains Mono) — preconnect já configurado
- CSS inline com variáveis (`:root { --bg, --orange, --pink, ... }`)
- SVG inline pra capa do hero (sem imagens externas)
- JS mínimo: só o snippet que injeta a `HOTMART_CHECKOUT_URL` nos botões de compra

**Por que assim:**

- Lighthouse 95+ em todas as métricas
- Zero ponto de falha de dependência
- Editável por qualquer dev sem setup
- Velocidade absoluta no mobile (audiência costuma abrir link do LinkedIn no celular)

**NÃO introduzir:**

- React, Vue, Svelte ou qualquer framework — quebra a tese
- Tailwind CDN (CSS atual já é compacto, adicionar Tailwind dobra o peso sem ganho)
- Webpack, Vite, qualquer build step — landing precisa ser editável e re-deployável em segundos
- Bibliotecas de animação pesadas (a animação atual é CSS puro `@keyframes float`)
- localStorage, cookies não-essenciais (só pixels/analytics consentidos)
- Imagens raster externas (mantém SVG inline)

## 3. Arquivos do repo

```
.
├── index.html        # landing completa — toda lógica vive aqui
├── README.md         # instruções de deploy
└── CLAUDE.md         # este arquivo
```

Não criar pastas adicionais sem motivo forte. Se precisar de assets binários (favicon, og-image), botar na raiz.

## 4. Variáveis críticas

Procure no fim do `index.html`:

```js
const HOTMART_CHECKOUT_URL = "#";
```

Quando o KYC do produto for aprovado pela Hotmart, essa string deve ser substituída pela URL real de checkout (formato `https://pay.hotmart.com/L105647550X`). Bruno vai informar quando estiver pronta.

Outras strings que podem mudar:

- Preço (atualmente R$ 397 / de R$ 497) — só alterar se Bruno confirmar nova precificação
- Cupom `EARLYBIRD30` — mencionado como "30% off por 7 dias"; se cupom mudar, atualizar copy
- Link do LinkedIn `linkedin.com/in/brunoonapps`

## 5. Princípios de copy

A copy foi escrita com voz autoral, anti-corporativês. Mantenha:

- **Frases curtas.** Parágrafos de 1-3 linhas máximo
- **Linguagem dev.** "tool call", "production", "ECONNREFUSED" são bem-vindos — o público entende
- **Honestidade.** A seção "NÃO é para você se" é deliberada — gera confiança, filtra leads ruins, reduz reembolso
- **Sem emoji excessivo.** O design do hero faz o trabalho visual; emoji em prosa quebra o tom técnico
- **Zero clichê de infoproduto.** Evite: "transforme sua vida", "segredos que ninguém te conta", "método X passos", "garanta o seu antes que acabe"

## 6. Tarefas comuns (em ordem de prioridade)

### 6.1 Atualizar `HOTMART_CHECKOUT_URL`
Quando Bruno informar a URL real, substituir `"#"` no script ao final. Re-deploy. Testar clicando nos 3 CTAs principais (topbar, hero, pricing card, final).

### 6.2 Adicionar depoimentos reais
Conforme primeiras vendas chegam, Bruno vai compartilhar feedback de leitores. Criar uma seção `<section class="testimonials">` antes do `<section class="pricing">`. Manter design minimalista — quote + nome + cargo. Sem foto inicialmente (sem foto fake).

### 6.3 Adicionar Open Graph
Após primeiro deploy estável, criar `og-image.png` (1200×630) reusando estética da capa. Adicionar tags meta `og:title`, `og:description`, `og:image`, `twitter:card="summary_large_image"`. Aumenta drasticamente CTR de links compartilhados.

### 6.4 Analytics
Quando Bruno autorizar, adicionar:
- **Plausible** ou **Umami** (sem cookies, LGPD-friendly) — preferência
- Ou **Google Analytics 4** se ele preferir
- Eventos: `cta_click`, `scroll_depth_50`, `scroll_depth_100`, `faq_open`

### 6.5 Pixels (só se rodarem tráfego pago)
- Pixel LinkedIn Insight Tag — alta probabilidade, audiência B2B dev
- Meta Pixel — só se Bruno fizer ads no Instagram/Facebook
- Carregar via `<noscript>` fallback e idealmente após interação (performance)

### 6.6 A/B test de headlines
Variantes de teste interessantes (depois de baseline estabelecido):
- Atual: "Construa agentes IA profissionais com Claude — do zero à produção."
- Variante B: "O guia técnico que falta entre 'tutorial de prompt' e 'agente em produção'."
- Variante C: "237 páginas de Claude Agent SDK + MCP — em PT-BR, sem fluff."

Implementar via cookie randomizado + log de qual variante converteu. **Não usar** ferramentas SaaS pesadas (Optimizely etc.) — solução em 30 linhas de JS basta.

### 6.7 Contador de vendas / FOMO
Só ativar com **30+ vendas reais**. Antes disso parece falso e queima credibilidade. Quando ativar, valor deve refletir contagem real (puxar via API Hotmart se permitir, ou Bruno atualiza manualmente em uma constante).

### 6.8 FAQ dinâmico
Conforme dúvidas chegam por e-mail/Hotmart, expandir a seção FAQ. Limite: 10 questões. Acima disso vira ruído.

## 7. Quando NÃO mexer sem perguntar

Mudanças que exigem confirmação explícita do Bruno:

- Alteração de preço, cupom, ou estrutura de oferta
- Mudança de headline principal (`<h1>`)
- Re-design grande (paleta, tipografia, layout)
- Adicionar campos de captura de e-mail (lead magnet) — depende de integração com mailing
- Remoção de qualquer seção existente

Mudanças que pode fazer sozinho:
- Bug fix de CSS/HTML
- Melhoria de microcopy mantendo o sentido
- Adição de meta tags
- Performance / acessibilidade
- Atualização de URL externa (LinkedIn, Hotmart, etc.)

## 8. Métricas que importam (e que não importam)

**Importa:**
- **Taxa de conversão visita→clique no CTA** (alvo: 8-15%)
- **Taxa de conversão clique no CTA→compra concluída** (alvo: 2-4%)
- **Bounce rate** abaixo de 60% indica copy/audiência alinhados
- **Tempo médio na página** acima de 90s indica que estão lendo
- **Mobile/Desktop split** — 60-70% mobile é esperado (LinkedIn é mobile-first)

**Não importa:**
- Pageviews absolutos (é landing, não blog)
- Lighthouse score acima de 95 (já está, não vale otimizar até 100 sacrificando UX)
- "Tempo de carregamento" abaixo de 1s (pena marginal por ganho marginal)

## 9. Deploy

Hospedagem: **Vercel** (preferência) ou Netlify. Push pra `main` deve disparar deploy automático.

Domínio: enquanto não há domínio próprio, usar URL `*.vercel.app` que o Vercel gera. Quando Bruno comprar domínio próprio, conectar via DNS.

## 10. Sinais para escalar / pivotar

Se em 2-4 semanas pós-lançamento:

- Conversão visita→checkout < 5% → revisar headline, oferta, social proof
- Bounce rate > 75% → tráfego desalinhado (rever fonte de tráfego antes de mexer na landing)
- Conversão > 12% → expandir investimento (tráfego pago, mais afiliados)

## 11. Contato

- **Bruno Santos:** brunosantos67040@gmail.com · linkedin.com/in/brunoonapps
- **Workspace fonte do bundle (não toque, é read-only pra esse repo):** `E:\dev\projects\livre-iniciativa-claude\livre-iniciativa-claude\`

## 12. Princípio guia

**Esta landing é uma ferramenta de venda, não um portfólio.** Toda mudança deve aumentar conversão ou clareza. Se uma "melhoria" não passa nesse filtro, não fazer.

Conversão acima de novidade. Clareza acima de criatividade. Velocidade acima de visual.
