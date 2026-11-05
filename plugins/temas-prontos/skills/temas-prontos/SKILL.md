---
name: temas-prontos
description: Aplica um tema completo — cores em tokens claro e escuro, par tipográfico, raios e forma — a uma página, app, slide ou documento, a partir de seis temas com contraste já conferido, ou cria um tema novo a partir de uma cor ou marca. Use quando a pessoa pedir "aplica um tema", "muda as cores", "quero uma paleta", "deixa com outra cara", "faz o modo escuro", "cria um tema a partir da minha marca", ou quando um projeto novo ainda não tem cores e fontes definidas.
---

# Temas prontos

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Um tema não é uma lista de cores bonitas: é um conjunto de **tokens com função**, que funciona no claro e no escuro e passa no contraste. Os seis temas em [temas.md](temas.md) já vêm assim. Esta skill escolhe, aplica e, quando nenhum serve, cria um novo do mesmo jeito.

## Escolher

1. Se o projeto já tem tokens de cor ou um design system, **não aplique tema por cima**. Pergunte se a pessoa quer trocar o tema do sistema inteiro ou só de uma peça.
2. Mostre os temas para a pessoa escolher. Se o ambiente permite, gere uma página HTML rápida com uma amostra por tema (título, parágrafo, botão principal, link e um card, no claro e no escuro) e mostre um print. Se não, liste nome, tom e para que combina, a partir de [temas.md](temas.md).
3. Espere a escolha. Não aplique um tema por conta própria.

## Aplicar

1. Leia o tema escolhido em [temas.md](temas.md).
2. Declare os tokens uma vez, no formato do projeto:

   ```css
   :root {
     --fundo: …; --superficie: …; --texto: …; --texto-2: …;
     --linha: …; --destaque: …; --sobre-destaque: …; --destaque-texto: …;
   }
   [data-theme="dark"] { /* os mesmos tokens com os valores do escuro */ }
   @media (prefers-color-scheme: dark) {
     :root:not([data-theme="light"]) { /* idem, para quem não escolheu */ }
   }
   ```

   No Tailwind, mapeie os tokens em `theme.extend.colors` apontando para as variáveis (`fundo: "var(--fundo)"`), para o escuro funcionar sem duplicar classes.
3. Troque **todas** as cores soltas do que você está tocando pelos tokens. Nenhum hex no meio dos componentes.
4. Carregue as fontes do tema com `display=swap` e só os pesos usados.
5. Aplique a forma do tema (raios, sombras ou linhas) junto com a cor. Cor nova com forma antiga parece remendo.

### Regras de uso dos tokens

- `destaque` é para **uma** ação principal por tela e para a marca. Não pinte títulos, ícones e bordas com ele.
- Texto sobre `destaque` usa sempre `sobre-destaque`.
- Link e texto em destaque usam `destaque-texto` (no Manchete claro, por exemplo, o amarelo não tem contraste como texto; o `destaque-texto` resolve).
- `texto-2` é para apoio: legendas, metadados, placeholders. Nunca para o conteúdo principal.
- `superficie` separa camadas (cards, menus, modais) do `fundo`. No escuro, a camada de cima é a mais clara.

## Criar um tema novo

Quando nenhum dos seis serve, ou a pessoa traz uma cor ou uma marca:

1. Parta da cor da marca como `destaque`. Se ela não tem contraste 4,5:1 sobre o fundo, crie um `destaque-texto` mais escuro (no claro) ou mais claro (no escuro) do mesmo matiz.
2. Derive os neutros do matiz da marca, levemente tingidos, em vez de cinza puro.
3. Monte as duas versões, clara e escura. O escuro não é o claro invertido: o fundo fica perto do preto tingido, o texto não é branco puro e o destaque costuma clarear.
4. Escolha o par tipográfico pelo tom (veja os exemplos em [temas.md](temas.md)): uma família para títulos com personalidade e uma para texto que leia bem em tamanho pequeno.
5. **Confira o contraste antes de mostrar.** Rode, por exemplo:

   ```js
   const lum = h => { const c = h.match(/\w\w/g).map(x => parseInt(x, 16) / 255).map(v => v <= .04045 ? v / 12.92 : ((v + .055) / 1.055) ** 2.4); return .2126 * c[0] + .7152 * c[1] + .0722 * c[2]; };
   const contraste = (a, b) => { const [x, y] = [lum(a), lum(b)].sort((p, q) => q - p); return (x + .05) / (y + .05); };
   // texto/fundo ≥ 7 · texto-2/fundo e texto-2/superficie ≥ 4,5 · sobre-destaque/destaque ≥ 4,5 · destaque-texto/fundo ≥ 4,5
   ```

6. Mostre o tema novo no mesmo formato da tabela de [temas.md](temas.md), com os números de contraste, e só aplique depois do ok.

## Checklist

- [ ] A pessoa escolheu o tema (ou aprovou o novo)?
- [ ] Os tokens estão declarados uma vez, com claro e escuro?
- [ ] Nenhuma cor solta sobrou nos componentes tocados?
- [ ] `destaque` aparece pouco; texto sobre ele usa `sobre-destaque`?
- [ ] Fontes carregadas só com os pesos usados?
- [ ] Contraste conferido nos dois modos?
