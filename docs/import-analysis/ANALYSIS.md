# Page Import Analysis — inter.co

> Análise gerada pelo skill **page-import** (AEM Edge Delivery Services).
> Fonte: https://www.inter.co · Capturado: 2026-07-16 · Gerador origem: Gatsby 5.16.1 (React SPA).
>
> ⚠️ **Contexto**: page-import produz conteúdo em formato canônico de blocos **EDS/Franklin**.
> O repositório atual (`ibcmed`) é **AEM as a Cloud Service** (Maven/HTL/Sling), não EDS.
> Por isso os passos 4 (gerar HTML EDS) e 5 (preview em dev server EDS) **não** foram executados —
> ficam como N/A. Este documento entrega a **análise** (scrape + estrutura + decisão de autoria).

## Conteúdo do diretório

| Arquivo | Descrição |
|---|---|
| `metadata.json` | Metadados (OG/Twitter/JSON-LD), paths, mapa de imagens |
| `screenshot.png` | Captura full-page (referência visual) |
| `cleaned.html` | HTML principal com caminhos locais de imagem |
| `images/` | 22 imagens baixadas (WebP/AVIF/SVG → PNG) |
| `ANALYSIS.md` | Este documento |

## Metadados

| Campo | Valor |
|---|---|
| Título | Inter: o Super App da sua vida financeira |
| Descrição | O Super App da sua vida financeira. Conta digital, cartão de crédito, shopping, assistente financeira com AI, investimentos... |
| Canonical | https://inter.co/ |
| Idioma | pt-BR |
| theme-color | #EA7100 (laranja Inter) |
| OG image | static.bancointer.com.br/.../open-graph_imagem.png |
| JSON-LD | Organization (Banco Inter) + WebPage |

Imagens: 38 detectadas · 21 convertidas · **25 falharam** — a maioria são *tracking pixels*
(Google Ads `1p-user-list`, ga-audiences), **não** conteúdo. Imagens reais de conteúdo baixadas OK.

## Escopo

Skill importa **conteúdo principal**. Header, navegação e footer são pulados (skills dedicadas).
Nav detectada (fora de escopo): Finanças · Estilo de vida · Segmentos · Vida Global · Loop · Acesse/Abra sua conta.

## Estrutura da página — 9 seções

Decisão de autoria por **David's Model**: preferir *default content* (heading/parágrafo/imagem/link
que um autor escreveria no Word) e só usar **bloco** quando a estrutura exige (grid, colunas, carrossel).

| # | Seção (heading) | Sequência de conteúdo | Decisão de autoria | Bloco EDS | Estilo de seção |
|---|---|---|---|---|---|
| 0 | **Hero** — H1 "O Super App da sua vida financeira" | Imagem lifestyle + H1 + CTA "Abra sua conta" | Default content (H1 + imagem + link) OU **Hero** se full-bleed | `hero` (opcional) | Highlight / laranja |
| 1 | H2 "Fácil, rápido e gratuito" → H3 "Cartão de crédito e conta digital pra você" | Linha de 3 fotos de pessoas ("Peça dele a partir de") + rótulos | **Bloco** — grid de cards | `cards` | Default |
| 2 | H2 "Novo Desenrola Brasil no Inter" | Banner promo + texto + CTA "Saiba mais" | Default content OU 2 colunas (imagem+texto) | `columns` | Highlight |
| 3 | H2 "Mais tempo. Mais inteligência pra sua vida." | Texto + assistente com AI + barra de busca + imagem app | **Bloco** — imagem + texto lado a lado | `columns` | Default |
| 4 | H2 "Conta PJ pra superar os desafios do seu negócio" | Imagem + texto + CTA "Conheça a Conta PJ" | 2 colunas (imagem+texto+CTA) | `columns` | Default |
| 5 | H2 "Sua vida global é Inter" | Card Global Account (imagem) + texto + CTA "Conheça a Global Account" | 2 colunas | `columns` | Highlight |
| 6 | H2 "Inter Shop com tudo pra você" | Imagem phone + texto + CTA "Acessar Inter Shop" | 2 colunas | `columns` | Default |
| 7 | H2 "Wearables. O futuro dos pagamentos chegou." | Grade/abas de dispositivos wearable + CTA "Conhecer Wearables" | **Bloco** — cards ou carrossel | `cards` ou `carousel` | Default |

## Inventário de blocos (Block Collection)

Blocos padrão suficientes para esta página (nenhum bloco local — projeto não é EDS):

| Bloco | Uso nesta página | Fonte |
|---|---|---|
| `hero` | Seção 0 (se full-bleed) | Block Collection |
| `cards` | Seções 1, 7 | Block Collection |
| `columns` | Seções 2–6 | Block Collection |
| `carousel` | Seção 7 (alternativa a cards) | Block Collection |

Nenhuma variante nova necessária — blocos usados como estão.

## CTAs / links principais (conteúdo)

Abra sua conta · Saiba mais · Conheça a Conta PJ · Conheça a Global Account · Acessar Inter Shop · Conhecer Wearables

## Próximos passos (só se destino for EDS)

4. `generate-import-html` → gerar `/index.plain.html` no formato canônico de blocos.
5. `preview-import` → subir dev server EDS (`aem up`) e comparar com `screenshot.png`.

Ambos exigem um **projeto EDS** (boilerplate aem.live + blocos). Este repo é AEM CS →
para reproduzir os componentes aqui, o caminho é a skill `create-component` (HTL/Sling), não blocos EDS.

## Limitações da análise

- SPA Gatsby: conteúdo renderizado via JS; scroll disparou lazy-load, mas seções muito
  abaixo da dobra podem ter carregado parcial.
- 25 imagens "falharam" = pixels de rastreamento, não conteúdo — ignoráveis.
- Header/nav/footer fora de escopo por design do skill.
