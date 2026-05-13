# Landing Page — Como publicar

Esta pasta contém uma landing page **standalone** (HTML único, sem build, sem dependências externas além de fontes do Google).

## Caminho mais rápido (5 minutos, deploy gratuito)

### Opção 1 — Vercel (recomendado)

1. Crie conta em https://vercel.com (login com GitHub).
2. Suba o conteúdo desta pasta como repositório no GitHub.
3. No Vercel, "Import Project" → seleciona o repo → "Deploy".
4. Vercel atribui um domínio `*.vercel.app` automático. Você pode plugar um domínio customizado depois.

### Opção 2 — Netlify

1. https://app.netlify.com/drop
2. Arraste a pasta inteira (apenas `index.html` é necessário).
3. Pronto. URL ativa em segundos.

### Opção 3 — Hospedagem própria

`index.html` é tudo que você precisa. Suba via FTP/SFTP em qualquer hospedagem.

## O que ajustar antes de divulgar

A URL do checkout Hotmart já vem **hardcoded** nos botões de CTA (`<a href="https://pay.hotmart.com/...">`). Não há script JS de injeção.

Se precisar trocar a URL (raro — apenas se a Hotmart emitir nova URL após mudança no produto):

1. Abra `index.html`
2. Busque por `pay.hotmart.com`
3. Substitua as 2 ocorrências (CTA principal do pricing + CTA final pós-FAQ)
4. Salve. Re-deploy.

## Métricas

A página não tem analytics embutido. Recomendado:

- **Google Analytics 4** — cole o snippet antes de `</head>`.
- **Plausible** ou **Umami** — alternativas sem cookies.
- **Hotmart Analytics** — já vem ativado no painel do produto e captura conversões.

## Otimizações futuras (opcionais)

- A/B teste de headline (ferramentas: VWO, Convert).
- Cole pixel do Meta/TikTok se for rodar tráfego pago.
- Adicione depoimentos reais (`<section class="testimonials">`) após primeiras vendas.
- Vídeo curto de apresentação no hero (substituir a capa estática).

## Performance

- Lighthouse esperado: 95+ em todas as métricas.
- Sem JS pesado, fontes via Google Fonts (preconnect já incluso).
- SVG inline, sem imagens externas.
