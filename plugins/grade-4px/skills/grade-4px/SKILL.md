---
name: grade-4px
description: Mantém todo espaçamento de interface numa grade de 4 px (ou 8 px) — margens, paddings, gaps, alturas de componentes e deslocamentos. Use ao escrever ou revisar CSS, Tailwind, estilos de componentes, tokens de espaçamento ou layout de qualquer tela, e quando a pessoa pedir "alinha isso", "o espaçamento está estranho", "segue a grade" ou "deixa mais organizado", mesmo que ela não diga "4px".
---

# Grade de 4 px

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Todo espaço entre coisas é múltiplo de 4. É o que faz uma tela parecer "arrumada" sem que ninguém saiba dizer por quê: os respiros se repetem, os alinhamentos batem e as decisões ficam previsíveis para quem desenha e para quem implementa.

## A régua

Use só estes valores para margin, padding, gap, inset, top/left/right/bottom, alturas e larguras fixas de componentes:

`0 · 4 · 8 · 12 · 16 · 20 · 24 · 32 · 40 · 48 · 56 · 64 · 80 · 96 · 128`

- Entre elementos de um mesmo grupo: 4 a 12.
- Entre grupos: 16 a 32.
- Entre seções: 48 a 128.
- Na dúvida entre dois valores, escolha o maior. Respiro raramente é o problema.

Nunca: 2, 3, 5, 6, 7, 9, 10, 14, 15, 18, 22, 30, 35, 45… Nem `rem` que dê fração de 4 (por exemplo `0.375rem` = 6 px).

## Onde a regra não vale

- Bordas e linhas: 1 px e 2 px.
- Tamanho de fonte: segue a escala tipográfica do projeto. A **altura de linha** em px, essa sim, fica em múltiplo de 4 quando dá (16/24, 14/20, 12/16).
- Ícones: 16, 20, 24, 32 já caem na grade; se o ícone for de outro tamanho, compense no container.
- Raio de borda: 4, 8, 12, 16 ou "pílula". Evite 6 e 10.
- Valores fluidos (`clamp`, `%`, `vw`) são aceitos quando a pessoa pede um layout fluido; os limites do `clamp` ficam na grade (`clamp(16px, 4vw, 32px)`).

## Como aplicar

1. **Antes de escrever:** veja se o projeto já tem tokens de espaçamento (CSS custom properties, tema do Tailwind, `spacing` do design system). Se tiver, use os tokens e não números soltos. Se não tiver e o arquivo for novo, proponha a régua acima como tokens (`--s-1: 4px` … ).
2. **No Tailwind:** a escala padrão já é de 4 px (`p-1` = 4, `p-2` = 8…). Evite os meios-passos `0.5`, `1.5`, `2.5`, `3.5` (2, 6, 10, 14 px) e valores arbitrários como `p-[10px]`.
3. **Ao herdar código fora da grade:** arredonde para o múltiplo de 4 mais próximo **só no que você está mexendo**, e diga o que mudou. Não reescreva o arquivo inteiro sem pedirem.
4. **Componentes com borda:** a borda conta. Um botão de 40 px de altura com 1 px de borda tem 38 px por dentro; acerte o padding vertical para o total fechar em múltiplo de 4.

## Conferência antes de entregar

Procure valores fora da grade no que você alterou:

```bash
grep -nE '(margin|padding|gap|inset|top|left|right|bottom|height|width)[^;]*[^0-9.](2|3|5|6|7|9|10|11|13|14|15|17|18|19|21|22|23|25|26|27|30|35|45)px' caminho/do/arquivo.css
```

No Tailwind: `grep -nE '\b(p|m|gap|space-[xy]|inset|top|left|right|bottom)[a-z]*-(0\.5|1\.5|2\.5|3\.5|\[[0-9]+px\])' -r src/`

Se sobrar algum valor de propósito (ajuste óptico, alinhamento com uma imagem), deixe um comentário curto explicando.
