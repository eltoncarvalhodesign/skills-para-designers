---
name: acabamento
description: Dá o acabamento que separa uma interface "funcionando" de uma interface que parece cara — estados de cada componente, microinterações, curvas e durações de movimento, foco, toque, carregamento e os detalhes invisíveis de tipografia e layout. Use ao finalizar ou revisar um componente ou tela, ao criar botões, menus, modais, toasts, abas e formulários, e quando a pessoa disser "falta capricho", "está duro", "parece amador", "dá um polimento", "a animação está estranha" ou "deixa mais gostoso de usar".
---

# Acabamento

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Acabamento é o último trecho do trabalho, o que ninguém pede e todo mundo sente. Uma tela pode estar certa no layout e ainda parecer amadora porque o botão não reage ao toque, o menu surge do nada ou o número pula de largura a cada atualização. Esta skill passa por esses pontos em ordem.

## 1. Cada componente tem todos os estados

Antes de achar que um componente está pronto, confira se ele tem:

| Estado | O que precisa |
|---|---|
| Repouso | O visual base, com contraste suficiente |
| Hover | Só em dispositivos com mouse: `@media (hover: hover) and (pointer: fine)` |
| Foco | Anel visível com `:focus-visible` (não `:focus`), 2 px, afastado 2 a 4 px do elemento |
| Pressionado | Resposta imediata ao toque ou clique, por exemplo `transform: scale(.98)` |
| Desabilitado | Visual apagado e motivo claro por perto; prefira `aria-disabled` quando a pessoa precisa entender por que não pode |
| Carregando | O botão mantém a largura, troca o rótulo por um indicador e não aceita segundo clique |
| Erro e vazio | Texto que diz o que aconteceu e o que fazer, com uma ação |

O estado que falta é quase sempre foco, carregando ou vazio.

## 2. Decida se deve animar

Movimento serve para explicar uma mudança: de onde algo veio, para onde foi, o que mudou de estado. Antes de animar, pergunte:

- **Quantas vezes por dia a pessoa vê isso?** Ação de teclado e coisas repetidas dezenas de vezes (abrir a busca, trocar de item numa lista) ficam sem animação ou quase. Coisas ocasionais (modal, gaveta, aviso) têm animação curta. Momentos raros (primeiro acesso, conclusão) podem ter um pouco de celebração.
- **O que ela explica?** Se a resposta é "fica bonito" e a coisa aparece toda hora, não anime.

## 3. Curvas e durações

Use poucos valores, definidos uma vez:

```css
:root {
  --curva-sai: cubic-bezier(.16, 1, .3, 1);     /* entradas: rápida no começo, assenta suave */
  --curva-move: cubic-bezier(.65, 0, .35, 1);   /* algo que se desloca na tela */
  --rapido: 120ms;   /* toque, hover, troca de cor */
  --medio: 200ms;    /* menus, tooltips, abas */
  --lento: 320ms;    /* gavetas, bottom sheets, modais */
}
```

- **Entrada usa curva que começa rápida.** A pessoa vê a resposta no mesmo instante. Curva que começa devagar (`ease-in`) parece atraso.
- **Saída é mais rápida que a entrada.** Quem fecha já decidiu; não faça esperar.
- **Interface fica abaixo de ~320 ms.** Animação longa parece lentidão, mesmo quando o sistema é rápido.
- **Transite propriedades nomeadas**, nunca `transition: all`.

## 4. Entradas e saídas

- **Nada surge do zero.** Comece de `opacity: 0` com um deslocamento pequeno (`translateY(4px)` a `8px`) ou escala perto de 1 (`.96`). Escala zero parece explosão.
- **Menus e popovers nascem do gatilho.** Ajuste `transform-origin` para o lado do botão que abriu. Modal centralizado pode crescer do centro.
- **Gavetas e sheets usam porcentagem**: `translateY(100%)` esconde pelo tamanho do próprio elemento, seja qual for a altura.
- **Prefira `transition` a `@keyframes` em coisas que podem ser interrompidas** (abrir e fechar rápido, avisos empilhados). A transição muda de rumo no meio; a animação por keyframes recomeça.
- Para entrada sem JavaScript, `@starting-style` resolve nos navegadores atuais.

## 5. Toque e gestos

- Alvo de toque com pelo menos 44 × 44 px. Se o visual é menor, aumente a área com um pseudo-elemento invisível.
- Arrastar para fechar: feche por distância **ou** por velocidade (um gesto rápido e curto também vale). Depois do limite, deixe o elemento resistir em vez de travar seco.
- Durante o arraste, capture o ponteiro (`setPointerCapture`) e ignore um segundo dedo.
- Nada importante só no hover: no toque, ele não existe.

## 6. Detalhes invisíveis

- **Números que mudam** usam `font-variant-numeric: tabular-nums`, para não dançar de largura.
- **Títulos** com `text-wrap: balance`; **parágrafos** com `text-wrap: pretty` (evita palavra sozinha na última linha).
- **Imagens** com `width`/`height` ou `aspect-ratio`, para o layout não pular ao carregar.
- **Modais e listas internas** com `overscroll-behavior: contain`, para a rolagem não vazar para a página.
- **Âncoras** com `scroll-margin-top` do tamanho do cabeçalho fixo.
- **Ícone e texto** alinhados pelo centro óptico, não só pela caixa; ajuste 1 px quando o olho pede.
- **Cursor** de mão só no que é clicável; texto selecionável onde a pessoa vai querer copiar.

## 7. Menos movimento

Com `prefers-reduced-motion: reduce`, troque deslocamento e escala por um fade curto ou pela troca direta de estado. Mantenha mudanças de cor e opacidade que ajudam a entender o que aconteceu.

## Como entregar uma revisão

Ao revisar um componente ou uma tela, responda em três blocos curtos:

1. **Corrigido:** o que você já ajustou, uma linha por item, com o trecho de código quando ajudar.
2. **Sugerido:** o que depende de decisão da pessoa (um efeito novo, uma mudança visível).
3. **Deixado como está:** o que parece problema mas está certo, e por quê.

## Checklist

- [ ] Todos os estados existem, inclusive foco, carregando e vazio?
- [ ] Cada animação explica uma mudança e não aparece em ação repetitiva?
- [ ] Entradas rápidas no começo, saídas mais curtas, tudo abaixo de ~320 ms?
- [ ] Nada nasce da escala zero; menus nascem do gatilho?
- [ ] Hover só com mouse; alvos de toque com 44 px?
- [ ] Números tabulares, títulos balanceados, imagens com proporção?
- [ ] Movimento reduzido respeitado?
