# leaomartins.com.br

Landing page de **Leão Martins** — desenvolvimento de software sob medida, criação de
sites e consultoria de TI. Objetivo único da página: converter visitante em conversa
no WhatsApp.

## Como funciona

Site estático de **um único arquivo**: [`index.html`](index.html), com CSS embutido e
um bloco pequeno de JavaScript vanilla (apenas o acordeão do FAQ). Sem build, sem
dependências — a única requisição externa é o Google Fonts (Sora + Manrope).

Para visualizar localmente, abra o arquivo no navegador ou rode:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Decisões técnicas

- **Ícones em SVG inline** (traço, `currentColor`). Nenhum emoji como elemento de design.
- **Sem animação decorativa** — só transições funcionais (hover, expandir do FAQ), e
  todas desligadas em `prefers-reduced-motion: reduce`.
- **Tema claro e escuro nativos** via `color-scheme: light dark` +
  `@media (prefers-color-scheme: dark)`, para o site controlar o modo escuro em vez do
  navegador aplicar inversão automática (que quebra o layout).
- A variável de **fundo de painel escuro** (`--panel`) é separada da variável de **cor de
  título** (`--ink`). Se forem a mesma, o modo escuro quebra e o título fica invisível.
  Botão sobre painel escuro usa fundo branco com texto escuro fixo (`.btn-onink`),
  nunca a variável de título.
- Mobile-first funcional: todos os grids colapsam para 1 coluna no celular.
- SEO básico: `title`, meta description, Open Graph, canonical.

## Paleta

| Token           | Claro     | Escuro    | Uso                                  |
| --------------- | --------- | --------- | ------------------------------------ |
| `--paper`       | `#F4F5F6` | `#0B1712` | Fundo da página                      |
| `--card`        | `#FFFFFF` | `#12241D` | Superfícies / cartões                |
| `--panel`       | `#0E2A22` | `#173328` | Seções escuras                       |
| `--ink`         | `#0E2A22` | `#F1F5F3` | Títulos                              |
| `--text`        | `#16231E` | `#C9D3CE` | Corpo de texto                       |
| `--muted`       | `#5B6670` | `#8B968F` | Texto secundário                     |
| `--accent`      | `#0FA678` | `#16C08A` | Acento gráfico                       |
| `--accent-deep` | `#0B7A57` | `#3ACB93` | Acento em texto                      |
| `--btn`         | `#0B7A57` | `#0B7A57` | Fundo do botão primário (texto `#fff`) |

WhatsApp mantém o verde de marca `#25D366`.

## Pendências antes de divulgar

A página está no ar com **placeholders explícitos**, marcados em amarelo/verde tracejado
na própria tela (`.fill-note`). Prova social inventada é o maior risco de credibilidade
que existe — nunca publicar texto fictício.

- [x] **Trabalhos** (`#trabalhos`): 4 projetos reais — Peixuxo, NOC Center, ISP Team e
      Link Lion.
- [ ] **Números nos cases**: os cartões descrevem o problema e o que foi construído, mas
      nenhum tem resultado quantificado (tanques monitorados, provedores usando, técnicos
      ativos, downloads). É o que mais converte — vale acrescentar quando houver o dado.
- [ ] **ispteam.com.br está retornando 403** (verificado do Brasil e de fora, é o Cloudflare
      do próprio domínio). Por isso o case do ISP Team está sem link. Religar o site e
      adicionar o `.case-link`.
- [ ] **Prints dos projetos**: as capas dos cases hoje são tipográficas. Screenshot real da
      tela converte mais.
- [x] **Depoimentos**: seção substituída por uma lista de clientes reais (`#clientes`),
      já que ainda não há depoimento coletado.
- [ ] **Autorização dos clientes**: confirmar com Link Internet, Net7, Recanto D3L,
      OneNext e I.E.R.C. que podem ser citados nominalmente no site.
- [ ] **Depoimentos de verdade**: quando houver, pedir uma frase por WhatsApp e publicar
      com nome e empresa reais — nunca texto fictício.
- [ ] **Imagem de compartilhamento**: criar uma imagem 1200×630 e adicionar
      `<meta property="og:image">`. Hoje a `twitter:card` está como
      `summary_large_image` sem imagem associada.
- [ ] Remover os blocos `.fill-note` (e a regra CSS correspondente) depois de preencher.

## Contato

WhatsApp (67) 99310-3403 — https://wa.me/5567993103403
