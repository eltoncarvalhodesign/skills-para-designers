---
name: site-leve
description: Mantém sites e interfaces leves e fluidos — anima só transform e opacity, evita repintar elementos grandes, carrega o pesado depois, pausa o que não está à vista e respeita quem prefere menos movimento. Use ao criar animações, transições, mapas, gráficos, fundos animados, listas longas, páginas com muitas imagens ou dados, e quando a pessoa disser "está travando", "pesado no celular", "esquenta o celular", "quero mais animação" ou "otimiza".
---

# Site leve

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Animação bonita que trava no celular é pior que nenhuma animação. Esta skill deixa o efeito e tira o custo. Vale em dobro para páginas que ficam abertas por muito tempo, rodam em TV ou em celular simples.

## Movimento

- **Anime só `transform` e `opacity`.** Eles rodam no compositor, sem recalcular layout nem repintar. Nada de animar `width`, `height`, `top`, `left`, `margin`, `box-shadow`, `filter: blur` grande ou cores de centenas de elementos por quadro.
- **Elemento grande e complexo (mapa, SVG com muitas formas, canvas) se move como imagem.** Durante o movimento, aplique `transform` no conjunto; redesenhe com detalhe uma vez só, no fim.
- **Destaques que se mexem (contornos, anéis, cursores) ficam numa camada própria e fina** por cima, não redesenhando o elemento de baixo.
- `will-change` só durante a animação e só no que anima; tire depois.
- Prefira transições curtas (150–300 ms) com `ease-out`. Animação longa parece lentidão.
- **`prefers-reduced-motion: reduce`**: troque movimento por troca simples de estado (ou um fade curto).

## Carregamento

- O que aparece primeiro carrega primeiro. Dados pesados, mapas detalhados, vídeos e bibliotecas grandes carregam depois da primeira pintura ou quando chegam perto da tela (`IntersectionObserver`, `loading="lazy"`, `import()` dinâmico).
- Imagens em AVIF/WebP, com `width` e `height` declarados (evita pulo de layout) e `srcset` para o tamanho certo.
- Fontes: no máximo 2 famílias, `font-display: swap`, subset quando der.
- Listas com centenas de itens: virtualize ou pagine.

## Enquanto a página está aberta

- **Pause tudo que é periódico quando a aba some** (`document.visibilitychange`): timers, polling, animações em loop, vídeos.
- Um `requestAnimationFrame` por vez, não um por componente.
- Escuta de scroll e resize com `passive: true` e com o trabalho pesado limitado (throttle ou rAF).

## Como trabalhar

1. **Ao propor um efeito, diga o custo** em uma linha ("esse brilho repinta o mapa inteiro a cada quadro; dá para fazer com uma camada por cima").
2. **Ao implementar,** escolha a versão compositor-only do efeito, mesmo que dê um pouco mais de trabalho.
3. **Antes de entregar,** grave 5 segundos no painel Performance do DevTools com CPU em 4× mais lento: procure quadros vermelhos, "Recalculate Style" e "Paint" grandes durante a animação. Se houver, o efeito ainda não está leve.

## Checklist

- [ ] Toda animação usa só `transform`/`opacity`?
- [ ] Nada grande é redesenhado a cada quadro?
- [ ] O pesado carrega depois da primeira pintura ou perto da tela?
- [ ] Timers e loops param com a aba escondida?
- [ ] `prefers-reduced-motion` respeitado?
- [ ] Imagens com tamanho declarado e formato moderno?
