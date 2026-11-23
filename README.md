# PESCADOR — Cozinha Caiçara

Landing page de alta conversão para um restaurante fictício em Arraial do Cabo, RJ:
cardápio interativo, pedido sem cadastro e finalização pelo WhatsApp.

> **Projeto demonstrativo.** Preços, depoimentos e o cardápio são fictícios. Endereço, horários
> e WhatsApp são placeholders ("A definir") e precisam ser preenchidos antes de publicar.

## Stack
React 18 · Vite 5 · Tailwind CSS 3 · mobile-first (celular, tablet e desktop) · sem backend.

## Requisitos
Node.js 18 ou superior.

## Instalação e execução
```bash
npm install
npm run dev        # http://localhost:5173
npm run build      # gera a pasta dist/
npm run preview    # testa o build localmente
```

## Estrutura
```
.
├── index.html                 # SEO (title, description, Open Graph, JSON-LD)
├── package.json
├── vite.config.js             # base './' (caminhos relativos)
├── tailwind.config.js · postcss.config.js
├── vercel.json
├── .env.example               # VITE_WHATSAPP
├── .github/workflows/deploy.yml
├── public/assets/images/      # fotografias e logo (caminhos relativos)
└── src/
    ├── main.jsx · App.jsx · index.css
    ├── config/site.js         # nome, endereço, WhatsApp, horários
    ├── data/menu.js           # produtos, preços, categorias, avaliações
    ├── data/photos.js         # fotos do hero, "sobre" e galeria
    ├── hooks/useCart.js       # estado do carrinho
    ├── lib/format.js · whatsapp.js
    └── components/            # Header, Hero, About, MenuSection, MenuCard,
                               # Highlights, Sharing, Gallery, Reviews, Location,
                               # Footer, CartDrawer, CartBar, WhatsAppFab, ...
```

## O que editar
| Quero alterar | Arquivo |
|---|---|
| Nome, endereço, horários, mensagem inicial | `src/config/site.js` |
| WhatsApp (DDI+DDD+número, só dígitos) | `.env` (`VITE_WHATSAPP`) ou `src/config/site.js` |
| Produtos, descrições, preços, categorias | `src/data/menu.js` |
| Fotografias | `src/data/photos.js` e campo `photo` em `menu.js` |

### Fotografias
Coloque os arquivos (JPG/WebP otimizados) em `public/assets/images/` e informe só o nome, por exemplo
`photo: 'moqueca.webp'`. Campos vazios exibem uma ilustração padrão. Use apenas imagens próprias ou com
licença comercial adequada. Todas as imagens usam `loading="lazy"` (exceto a do hero).

## Publicação

### GitHub Pages
1. Envie o projeto para um repositório (branch `main`).
2. **Settings → Pages → Source: GitHub Actions**.
3. (Opcional) **Settings → Variables → Actions**: crie `VITE_WHATSAPP` com o número.
4. Cada push na `main` publica o site automaticamente.

### Vercel
Importe o repositório em vercel.com. O framework Vite é detectado (`vercel.json` incluso).
Defina `VITE_WHATSAPP` em **Settings → Environment Variables**.

## Acessibilidade e SEO
Navegação por teclado, foco visível, rótulos ARIA, `prefers-color-scheme` e `prefers-reduced-motion`,
meta tags, Open Graph e dados estruturados `Restaurant` com localidade Arraial do Cabo, RJ.

### Cloudflare Pages (integração Git)
O projeto é um site estático (React + Vite) e usa o build nativo do Pages. **Não é um Worker.**

| Campo | Valor |
|---|---|
| Framework preset | Vite |
| Root directory | `/` (a pasta que contém `package.json` e `index.html`) |
| Build command | `npm run build` |
| Build output directory | `dist` |
| Deploy command | **vazio** (não use `npx wrangler deploy`) |
| Variável | `NODE_VERSION=20` (ou superior), opcional `VITE_WHATSAPP` |

Não há `wrangler.toml`/`wrangler.jsonc` neste repositório de propósito: `wrangler deploy` publica Workers e falha
com "Missing entry-point to Worker script or to assets directory" em um projeto Pages.

Como saber se o projeto é Pages ou Worker: no painel, **Workers & Pages** lista o tipo de cada projeto.
Se estiver como Worker (ou com "Deploy command" preenchido em **Settings → Builds**), apague o comando de deploy
ou recrie o projeto em **Create → Pages → Connect to Git**.
