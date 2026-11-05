---
name: direcao-de-arte
description: Define uma direção de arte antes de desenhar ou codar uma página nova — assunto, público, tom, tipografia, cor, forma e um único ponto de ousadia — para fugir do visual genérico de IA sem atropelar o design system que já existe. Use ao criar landing pages, sites, portfólios, telas de marketing ou um produto do zero, ao "repaginar" algo existente, e quando a pessoa disser "está com cara de template", "parece feito por IA", "quero algo com personalidade", "sem graça" ou "me dá uma direção visual". Não use para ajustes pequenos em telas que já seguem um design system.
---

# Direção de arte

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Sem direção, o modelo entrega a média de tudo que já viu: o mesmo hero, os mesmos cards, a mesma paleta. A saída não é "ser criativo" no código; é decidir a direção **antes** do código, por escrito, e depois construir com disciplina.

## Primeiro: existe um design system?

- **Sim, e a tarefa é uma tela do produto:** a direção é o design system. Use os componentes e tokens dele, não invente fonte nem cor. Esta skill só ajuda a escolher a hierarquia e o momento de destaque dentro do que já existe.
- **Sim, mas a pessoa quer uma peça especial** (campanha, lançamento, página de evento): proponha a direção como uma variação do sistema, mantendo a família tipográfica ou a cor da marca, e diga o que muda.
- **Não existe:** siga o processo abaixo.

## O processo em quatro passos

### 1. Entenda o assunto

Responda em uma linha cada, e confirme com a pessoa se algo for suposição:

- **O que é** (produto, serviço, pessoa, evento)?
- **Para quem**, e em que situação a pessoa vai abrir a página?
- **Qual é a única coisa** que a página precisa fazer (entender, confiar, comprar, se inscrever)?
- **De que mundo** isso vem? Materiais, lugares, objetos, jargão, épocas. É daqui que saem as escolhas visuais que não parecem template: uma padaria, um escritório de advocacia e um app de corrida pedem mundos diferentes.

### 2. Proponha duas direções curtas

Escreva duas direções diferentes entre si, cada uma com:

```
Nome: (duas ou três palavras)
Tom: três adjetivos
Tipografia: família(s) e papel de cada uma (títulos, texto, números)
Cor: 4 a 6 cores com hex e função (fundo, texto, apoio, destaque)
Forma: raios, linhas, sombras, densidade
Imagem: foto, ilustração, 3D, só tipografia?
Movimento: onde, quanto e por quê
Ousadia: o único elemento que vai ser lembrado
```

Mostre as duas lado a lado e deixe a pessoa escolher ou misturar. Não comece a codar antes disso.

### 3. Teste contra o piloto automático

Releia a direção escolhida e marque tudo o que você colocaria em **qualquer** página parecida. Cada item marcado precisa de um motivo ligado ao assunto, ou sai. Sinais comuns de piloto automático:

- Degradê roxo e azul, ou fundo escuro com um verde-neon solitário, sem relação com o assunto.
- Hero com título genérico ("Transforme seu negócio"), subtítulo de duas linhas e dois botões.
- Três colunas de benefícios com ícone em círculo, todas do mesmo tamanho.
- Tudo dentro de cards iguais, mesmo raio e mesma sombra, sem hierarquia.
- Rótulo pequeno em maiúsculas acima de cada título, numeração 01/02/03 em conteúdo que não é sequência.
- Animação de "aparecer subindo" em cada seção da página.
- Emoji fazendo papel de ícone; fotos de banco com pessoas apontando para notebooks.

Algum desses pode ser a escolha certa. O problema é quando ele aparece por hábito.

### 4. Construa com disciplina

- **Uma ousadia só.** O elemento memorável ganha espaço; o resto fica calmo e alinhado.
- **Tipografia faz o trabalho.** Uma família bem usada (pesos, tamanhos, espaçamento) vale mais que três. Se usar duas, que sejam claramente diferentes. Linhas de texto com até ~75 caracteres.
- **Cor com função.** Cada cor tem um papel; o destaque aparece pouco para continuar sendo destaque.
- **Estrutura que informa.** Bordas, números, divisórias e rótulos só quando dizem algo sobre o conteúdo.
- **Movimento que responde.** Prefira um único momento coreografado (ou nenhum) a efeitos espalhados. Animação que responde a um clique é bem-vinda.

## O piso de qualidade (não negociável)

A direção pode ser ousada; a página não pode ser frágil:

- Responsiva até 375 px, com cara de app no celular.
- Contraste de texto AA (4,5:1; 3:1 para texto grande).
- Foco visível no teclado.
- Tema escuro, se o produto tiver, pensado junto e não invertido no fim.
- `prefers-reduced-motion` respeitado.
- Espaçamentos numa grade de 4 px.

## Texto também é direção

O texto deixa uma página com cara de template tão rápido quanto o visual.

- Escreva com o vocabulário de quem usa, não de quem construiu.
- Botão diz o que acontece: "Agendar visita", não "Enviar". A mesma ação mantém o mesmo nome do botão até a confirmação ("Agendar" → "Visita agendada").
- Erro diz o que houve e como resolver, sem pedir desculpas e sem ser vago.
- Sem conteúdo real? Escreva um texto plausível do assunto, nunca "Lorem ipsum" nem frases de efeito vazias.

## Ao entregar

Mostre um print (ou descreva) do resultado e, em três linhas: a direção escolhida, a ousadia e o que você cortou para manter a página calma.
