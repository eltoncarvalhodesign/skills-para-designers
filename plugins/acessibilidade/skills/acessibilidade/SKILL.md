---
name: acessibilidade
description: Garante que a interface funcione para todo mundo — contraste, teclado, foco, leitor de tela, formulários, toque, movimento e zoom — e revisa telas existentes com uma auditoria rápida e priorizada. Use ao criar ou revisar qualquer tela, componente, formulário, modal, menu ou gráfico, antes de entregar uma PR de interface, e quando a pessoa disser "está acessível?", "passa no WCAG?", "faz uma auditoria", "funciona com leitor de tela?" ou "navega pelo teclado?".
---

# Acessibilidade

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Acessibilidade não é uma etapa no fim: é parte de "estar pronto". Quase tudo se resolve com HTML certo, contraste suficiente e foco visível. Esta skill cuida disso enquanto você constrói e faz uma auditoria curta quando a tela já existe. A meta é o nível AA das WCAG 2.2.

## Ao construir

**HTML antes de ARIA**
- Botão é `<button>`, link é `<a href>`. Link leva a outro lugar; botão faz algo aqui. Nunca `<div onclick>`.
- Um `<h1>` por página e títulos em ordem (`h2` → `h3`), sem pular nível por causa do tamanho visual.
- Regiões com `<header>`, `<nav>`, `<main>`, `<footer>`; um link "Pular para o conteúdo" no começo.
- Listas são `<ul>`/`<ol>`; tabelas de dados são `<table>` com `<th scope>`.
- ARIA só quando o HTML não tem o elemento (abas, combobox, árvore). ARIA errado é pior que nenhum.

**Contraste**
- Texto normal: 4,5:1. Texto grande (24 px, ou 18,66 px em negrito): 3:1.
- Ícones que carregam sentido, bordas de campos e o anel de foco: 3:1 contra o fundo.
- Confira no claro **e** no escuro. Placeholder também é texto.

**Teclado e foco**
- Tudo que se clica se alcança com Tab, na ordem visual, e se aciona com Enter ou Espaço.
- Foco sempre visível (`:focus-visible`), com contraste e sem ficar escondido sob cabeçalho fixo (`scroll-padding-top`).
- Modal prende o foco dentro, fecha com Esc e devolve o foco ao botão que abriu. `<dialog>` com `showModal()` faz quase tudo isso sozinho.
- Menus e abas: setas navegam entre itens, Tab sai do grupo.

**Leitor de tela**
- Imagem com sentido tem `alt` que diz o que ela comunica; imagem decorativa tem `alt=""`.
- Botão só com ícone tem nome: `aria-label="Fechar"` ou texto escondido visualmente.
- Mudanças que acontecem sem recarregar (toast, "Salvo", erro de envio) são anunciadas com `role="status"` ou `aria-live="polite"`.
- O idioma da página está certo (`<html lang="pt-BR">`).

**Formulários**
- Todo campo tem `<label>` visível e ligado a ele. Placeholder não substitui label.
- Erro aparece junto ao campo, em texto (não só em cor), ligado com `aria-describedby`, e o campo recebe `aria-invalid="true"`.
- Campos com `autocomplete` e `inputmode` certos; obrigatório marcado em texto, não só com asterisco colorido.
- Ao enviar com erro, leve o foco ao primeiro campo com problema ou a um resumo no topo.

**Cor, toque, movimento e zoom**
- Cor nunca é o único sinal: erro tem ícone ou texto; link no meio do texto tem sublinhado.
- Alvos de toque com pelo menos 24 × 24 px (o ideal é 44 × 44) e espaço entre eles.
- `prefers-reduced-motion` respeitado; nada pisca mais de 3 vezes por segundo; vídeo e carrossel automáticos têm pausa.
- A página funciona com zoom de 200% e em 320 px de largura sem rolagem lateral.

**Gráficos e dados**
- Gráfico tem um resumo em texto (a conclusão) e, quando possível, a tabela com os números.
- Séries se distinguem por forma, rótulo ou padrão, não só por cor.

## Auditoria rápida (tela existente)

Faça nesta ordem e anote o que encontrar:

1. **Teclado:** percorra a tela inteira só com Tab, Shift+Tab, Enter, Espaço e Esc. Alguma coisa ficou inalcançável, sem foco visível ou presa?
2. **Contraste:** meça texto principal, texto secundário, placeholder, botões e bordas de campo, nos dois temas.
3. **Estrutura:** liste os títulos e as regiões da página. A hierarquia faz sentido lida sozinha?
4. **Nomes:** todo botão, link, campo e imagem tem um nome que faz sentido fora de contexto? ("Saiba mais" repetido cinco vezes não faz.)
5. **Formulário:** envie vazio. Os erros aparecem em texto, junto aos campos, e são anunciados?
6. **Zoom e largura:** 200% de zoom e 320 px de largura.
7. **Automático:** se o projeto tiver Playwright ou Cypress, rode o axe-core na página; se não, use o Lighthouse. O automático pega uns 30–40% dos problemas, por isso ele vem por último, não primeiro.

## Como relatar

Agrupe por gravidade e diga sempre onde está e como corrigir:

- **Bloqueia:** alguém não consegue concluir a tarefa (sem acesso por teclado, campo sem label, modal que prende sem saída).
- **Atrapalha:** dá para concluir, com esforço (contraste baixo, foco fraco, nome confuso).
- **Melhoria:** refinamentos (ordem de leitura, anúncio que poderia ser mais claro).

Corrija o que for técnico e reversível; traga para a pessoa só o que muda o visual ou o texto.

## Checklist

- [ ] HTML semântico, títulos em ordem, regiões e link de pular?
- [ ] Contraste AA no claro e no escuro, inclusive placeholder e bordas?
- [ ] Tudo alcançável por teclado, com foco visível e modais que devolvem o foco?
- [ ] Imagens, ícones e botões com nome; mudanças anunciadas?
- [ ] Campos com label, erros em texto ligados ao campo?
- [ ] Cor não é o único sinal; alvos de toque com tamanho; movimento reduzido?
- [ ] Funciona com 200% de zoom e em 320 px?
