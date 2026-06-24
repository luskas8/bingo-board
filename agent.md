# Bingo Board Acessível — Diretrizes do Projeto

## O que é este projeto

Painel de Bingo digital interativo, projetado para exibição em **telões e projetores**, com foco em **acessibilidade para pessoas com mais de 60 anos**. Funciona como uma página única (SPA) sem dependências externas além do Google Fonts.

---

## Arquitetura

| Arquivo | Descrição |
|---|---|
| `Bingo Board.dc.html` | Componente principal — toda a lógica, layout e interatividade |
| `favicon.svg` | Ícone do site (5 barras coloridas B-I-N-G-O) |

O projeto usa o sistema **Design Components (DC)**: arquivo `.dc.html` único com template HTML + classe JavaScript (`DCLogic`), sem bundler, sem framework externo.

---

## Estrutura do Tabuleiro

- **5 colunas:** B · I · N · G · O
- **15 números por coluna, top-down:**
  - B: 1–15 | I: 16–30 | N: 31–45 | G: 46–60 | O: 61–75
- **Total:** 75 células numéricas clicáveis

---

## Diretrizes de Design

### Tipografia
- Fonte: **Inter** (Google Fonts), pesos 700–900
- Tamanhos com `clamp()` + `vw` para escalar automaticamente com o projetor
- Texto nunca abaixo de `18px`; células com `clamp(18px, 2.3vw, 46px)`

### Contraste (WCAG 2.1 AAA — mínimo 7:1)
- Tema escuro: fundo `#0c0c0f`, texto `#ededf2` sobre cinza `#1d1d24`
- Tema claro: fundo `#f7f8fc`, texto `#0a1a3f` sobre branco `#ffffff`

### Cores das colunas (headers)
| Coluna | Cor |
|---|---|
| B | `#1565ff` — azul |
| I | `#e02020` — vermelho |
| N | `#7a3ff0` — roxo |
| G | `#0a9d3a` — verde |
| O | `#ff8c00` — laranja |

### Estado "Marcado" — mudança visual drástica
| Tema | Fundo | Texto | Extra |
|---|---|---|---|
| Escuro | `#d8ff00` (verde-limão neon) | `#0a0a0a` | Brilho externo (glow) + borda branca |
| Claro | `#0033e6` (azul elétrico) | `#ffffff` | Sombra azul + borda escura |

---

## Funcionalidades

- **Marcar/desmarcar** número ao clicar (toggle)
- **Último Número Chamado** exibido em tamanho gigante no topo central
- **Contador de marcados** (X de 75)
- **Reset com confirmação** (dois cliques para evitar acidente)
- **Alternância Tema Claro/Escuro** via botão no topo

---

## Acessibilidade

- `aria-pressed` em cada célula (estado sorteado/não sorteado)
- `aria-live="polite"` no painel do último número chamado
- `aria-label` descritivo em cada número: _"Número 7, coluna B, sorteado"_
- `style-focus` com outline laranja `#ff8c00` em todos os elementos interativos
- Áreas de clique grandes (células ocupam todo o espaço disponível na coluna)
- Sem animações que causem desconforto visual

---

## Responsividade

- `height: 100vh`, sem scroll vertical no telão
- Grid com `minmax(66px, 1fr)` e `overflow-x: auto` para scroll horizontal em mobile
- Headers e células escalam proporcionalmente via `clamp()` e `vw/vh`

---

## Próximas funcionalidades sugeridas

- [ ] Anúncio por voz via Web Speech API
