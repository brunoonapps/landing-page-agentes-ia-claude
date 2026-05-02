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

Abra `index.html` e procure:

```js
const HOTMART_CHECKOUT_URL = "#";
```

Substitua `"#"` pela URL real de checkout que a Hotmart te dá após publicar o produto. Exemplo:

```js
const HOTMART_CHECKOUT_URL = "https://pay.hotmart.com/B12345678X?checkoutMode=10";
```

Salve. Re-deploy. Os botões de compra agora levam ao checkout direto.

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
