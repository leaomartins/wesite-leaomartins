# Prompt — Landing page Leão Martins

Use este texto como instrução para qualquer IA de código (ou como especificação
para você mesmo) recriar/evoluir a landing page.

---

## Objetivo
Gerar uma landing page de **um único arquivo HTML** (sem framework, sem build),
para um desenvolvedor/consultor de TI que presta serviços. A página existe para
**converter visitante em conversa no WhatsApp**, estabelecendo credibilidade.

## Público
Donos de pequenas e médias empresas, muitas vezes não técnicos, que precisam de
software sob medida, site ou consultoria e querem confiar em quem contratam.

## Marca
- Nome: **Leão Martins**
- Site: leaomartins.com.br
- Base: Mato Grosso do Sul, atende todo o Brasil (remoto e presencial)
- Contato principal: WhatsApp (67) 99310-3403 → link `https://wa.me/5567993103403`
  com mensagem pré-preenchida.
- Monograma: "LM".

## Restrições técnicas
- **HTML único**, CSS embutido em `<style>`, JS mínimo em vanilla (só o acordeão do FAQ).
- Sem bibliotecas externas, exceto Google Fonts.
- Fontes: **Sora** (títulos) + **Manrope** (corpo).
- **Ícones em SVG** (traço, `currentColor`). Proibido emoji como elemento de design.
- **Sem animação decorativa.** Só transições funcionais (hover de botão/cartão,
  expandir do FAQ). Respeitar `prefers-reduced-motion`.
- **Temas claro e escuro nativos** via `@media (prefers-color-scheme)` e
  `color-scheme: light dark` — para o site controlar o modo escuro em vez do
  navegador aplicar inversão automática (que quebra o layout).
- Responsivo (mobile-first funcional): grids colapsam para 1 coluna no celular.
- SEO básico: title, meta description, Open Graph, canonical.

## Paleta (tokens CSS)
**Claro:** fundo `#F4F5F6`; superfície `#FFFFFF`; painéis escuros/texto-título
`#0E2A22`; corpo `#16231E`; secundário `#5B6670`; acento gráfico `#0FA678`;
acento em texto `#0B7A57`; botão primário `#0B7A57` com texto branco.

**Escuro:** fundo `#0B1712`; superfície `#12241D`; painéis `#173328`; títulos
`#F1F5F3`; corpo `#C9D3CE`; secundário `#8B968F`; acento `#16C08A`; acento em
texto `#3ACB93`. WhatsApp mantém verde de marca `#25D366`.

Regra: separar a variável de **fundo de painel escuro** da variável de **cor de
título**, senão o modo escuro quebra (título vira invisível). Botão sobre painel
escuro = fundo branco com texto escuro fixo (não usar a variável de título).

## Estrutura da página (nesta ordem)
1. **Header fixo** — monograma + nome à esquerda; navegação; CTA WhatsApp à direita.
2. **Herói** — título forte e específico com uma palavra em destaque; subtítulo que
   nomeia a dor real (processo manual, planilha, sistema travado); CTA primário
   (WhatsApp) + secundário (ver trabalhos); cartão lateral escuro com 3 diferenciais.
3. **Faixa de confiança** — 4 itens curtos com ícone.
4. **Serviços** — 6 cartões: software sob medida, criação de sites, landing pages,
   consultoria de TI, automação de processos, manutenção e evolução.
5. **Como funciona** — seção escura, 4 passos numerados (diagnóstico → proposta e
   escopo → desenvolvimento → entrega e evolução).
6. **Trabalhos/cases** — 3 cartões. **PLACEHOLDER claramente marcado**: substituir
   por projetos reais (problema → o que foi feito → resultado concreto com número).
7. **Depoimentos** — 2 cartões. **PLACEHOLDER claramente marcado**: só usar
   depoimentos reais, com nome e empresa. Nunca texto fictício no ar.
8. **FAQ** — acordeão com objeções reais (preço, atendimento remoto, prazo,
   suporte pós-entrega, melhorar site existente).
9. **CTA final** — seção escura centralizada com WhatsApp + telefone.
10. **Rodapé** — marca, navegação, contato.
11. **Botão flutuante de WhatsApp** fixo no canto.

## Copy (princípios)
- Específica e orientada a resultado; nada de buzzword genérica ("soluções
  digitais", "sinergia"). Falar da dor do cliente e do que ele ganha.
- Português do Brasil, tom profissional e direto.

## Regra inegociável de prova social
Nunca inventar depoimentos, nomes de clientes, logos ou números. As seções de
prova entram como placeholders explícitos, para o dono preencher com material real.
