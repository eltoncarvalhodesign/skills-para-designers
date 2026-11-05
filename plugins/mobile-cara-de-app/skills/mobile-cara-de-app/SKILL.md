---
name: mobile-cara-de-app
description: Faz a versão de celular de um site parecer um app nativo, não um site encolhido — bottom sheets no lugar de selects e modais, botões de largura total na zona do polegar, linhas grandes de toque, estados vazios de app, áreas seguras do iPhone. Use ao criar ou revisar layout responsivo, telas em 375–430 px, modais, filtros, seletores e formulários no celular, e quando a pessoa disser "no celular está quebrado", "parece jogado", "sem hierarquia no mobile" ou "quero com cara de app".
---

# Mobile com cara de app

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

No celular, as pessoas comparam o seu site com os apps que usam o dia todo. Um layout de desktop espremido parece quebrado mesmo quando "funciona". Esta skill traz os padrões que fazem a tela parecer nativa.

## Padrões

**Bottom sheet no lugar de select, menu e modal**
- Escolhas com mais de 4 opções, filtros e diálogos sobem de baixo, ocupando até ~90% da altura.
- Têm alça no topo (36 × 4 px, centralizada), fecham ao arrastar para baixo, ao tocar fora e com o botão voltar.
- Lista longa dentro do sheet rola por dentro; o cabeçalho e o botão de confirmar ficam fixos.
- Não use o `<select>` nativo para listas longas de opções (estados, países, categorias).

**Botões e ações**
- Ação principal em largura total, com 48 a 56 px de altura, presa ao rodapé quando é a ação da tela (`position: sticky; bottom: 0` com o fundo da página atrás).
- Nunca deixe botão no meio de uma frase ("Escolha seu [estado] para continuar"). A frase vira título e o botão vira uma linha ou um botão inteiro.
- Alvo de toque mínimo de 44 × 44 px, com 8 px entre alvos.

**Listas e linhas**
- Linhas de lista com 48 a 64 px, ícone ou avatar à esquerda, texto em 1–2 linhas, chevron ou valor à direita.
- A linha inteira é tocável, não só o texto.

**Estado vazio de app**
- Ícone, título curto, uma linha de explicação e um botão principal. Centralizado na área disponível.
- Nada de texto solto do tipo "Nenhum resultado encontrado." no canto.

**Detalhes que denunciam site encolhido**
- Campos de formulário com fonte de 16 px no mínimo (abaixo disso o iOS dá zoom).
- `inputmode` e `autocomplete` certos (`email`, `tel`, `numeric`) para abrir o teclado certo.
- Use `100dvh`, não `100vh`, para telas cheias.
- Respeite as áreas seguras: `padding-bottom: max(16px, env(safe-area-inset-bottom))` no rodapé fixo, e `viewport-fit=cover` na meta viewport.
- Hover não existe: tudo que aparece no hover precisa de outro caminho no toque.
- Sem rolagem horizontal na página. Carrosséis horizontais são intencionais e mostram um pedaço do próximo item.

## Como trabalhar

1. Desenhe o celular como tela própria, começando pelo que a pessoa faz com o polegar, não como o desktop reorganizado.
2. Teste em 375 px de largura (e numa tela baixa, 375 × 667) antes de entregar.
3. Ao revisar, liste os problemas com o padrão que resolve cada um ("select de estados → bottom sheet com busca").

## Checklist

- [ ] Selects longos e modais viraram bottom sheet?
- [ ] A ação principal está na zona do polegar, em largura total?
- [ ] Nenhum botão no meio de texto corrido?
- [ ] Alvos com 44 px ou mais e linhas inteiras tocáveis?
- [ ] Estados vazios com ícone, título, linha e botão?
- [ ] Inputs com 16 px, teclado certo e áreas seguras respeitadas?
