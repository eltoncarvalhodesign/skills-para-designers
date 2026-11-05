# Frontend com o Claude Code: um processo para designers

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

> Versão interativa, com o fluxo navegável, o simulador, o gerador de prompt e a skill para baixar: https://eltoncarvalho.com.br/processo/

O processo e o método que usei em mais de 30 PRs de design system e dark mode em produção, e o que aprendi fazendo. Quem é designer decide produto, visual e padrão. O Claude faz o papel de dev sênior e executa código, testes e evidência. A engenharia revisa e faz o merge.

## A ideia em uma frase

Cada card vira **uma sessão do Claude, numa worktree própria, com um prompt de entrada claro e dois pontos de parada**: o plano e a evidência. O resto (código, validação, prints, testes, PR) o Claude executa e mostra. Commit e PR, só quando você pede.

## Divisão de papéis

| Você decide | O Claude decide e executa |
|-|-|
| Escopo do card e o que fica de fora | Organização técnica (arquivos, commits, ordem) |
| Visual, padrão, comportamento que o usuário vê | Qual componente do design system usar, tokens, refactor seguro |
| Aprovar o plano antes de editar | Validações (lint, tipos, testes, E2E, performance) |
| Aprovar a evidência (prints antes e depois) | Prints, comparativos, registro da evidência |
| Pedir commit e PR | Abrir a PR no padrão do time e mover o card |
| Conduzir a conversa com quem revisa e decidir o que muda | Corrigir os apontamentos do bot de revisão e aplicar o que você combinar |

O que mais muda o resultado é deixar explícita a **fronteira de decisão**: o Claude resolve sozinho o que é técnico e reversível e me consulta quando a decisão é de produto, de visual, envolve outra pessoa ou não tem volta.

## O que você precisa

- **Claude Code**, de preferência no app desktop (sessões, worktrees, navegador e terminal no mesmo lugar).
- **Acesso ao repositório** e alguém da engenharia para revisar e fazer o merge.
- **Um design system** com componentes e tokens semânticos, ou pelo menos os tokens.
- **O ambiente local rodando** na sua máquina. A primeira configuração é a parte mais trabalhosa: vale fazer junto com alguém da engenharia.
- **Conectores**, se o time usa: gerenciador de tarefas, Figma, GitHub e o navegador do app (ou Playwright) para prints e E2E.
- **Regras do repo** (`AGENTS.md`, `CLAUDE.md`). O Claude já lê; o seu papel é cobrar quando ele desviar.

## Adapte ao seu time

O método é o mesmo em qualquer projeto. O que muda é o que cada time já tem. Defina uma vez e coloque na [skill](#a-skill) e no prompt de entrada.

| Item | Exemplo |
|-|-|
| Branch principal | `main` |
| Design system | pacote, e onde estão as regras dele |
| Biblioteca alternativa | o que usar quando o design system não tem o componente |
| Gerenciador de tarefas | Linear, Jira, GitHub Issues; qual status é "em revisão" |
| Padrão de branch | `usuario/id-do-card-titulo-em-kebab` |
| Padrão de PR | título, labels, pronta ou draft |
| Setup de uma worktree nova | install e build das bibliotecas internas |
| Subir o ambiente local | o comando ou script do time |
| Validações | lint, tipos do pacote, testes, código morto |
| Documentação | se mudança visível ao usuário leva página de docs |
| Bot de revisão | o nome, se houver |
| Pedido de revisão | canal e formato da mensagem |

## O fluxo de uma PR

Dez passos em quatro fases.

### Preparar

1. **Card pequeno.** Título curto (uns 40 caracteres), escopo claro e uma lista do que **não** mexer. Uma PR por card. Se o escopo crescer no meio, vira outro card.
2. **Sessão e worktree próprias.** Uma sessão por card, com o nome do card, para você achar cada uma na barra lateral (ex.: `DS-14 PR 3: campos do cadastro`). E uma worktree nova, a partir da branch principal atualizada: nunca uma branch velha, que mostra telas que não existem mais. O Claude roda o setup da worktree.
3. **Prompt de entrada.** Em vez de explicar a tarefa de cabeça a cada vez, você cola um prompt com o objetivo, a referência visual, o que fica de fora, as regras e os pontos de parada. [Modelo](#modelo-de-prompt-de-entrada) no fim.
4. **Ponto de parada 1: o plano.** Antes de editar, o Claude manda o plano: arquivos, componentes que vai usar, o que fica igual, riscos. Você aprova ou corrige. É o passo que mais evita retrabalho.

### Construir

5. **Construção, com regras fixas.**
   - **Design system primeiro.** Biblioteca alternativa só quando o design system não tem; nunca componente marcado como rascunho.
   - **Não reconstruir o que já existe.** Se você aponta uma tela como referência, o Claude usa o mesmo componente e ajusta só por props e classes. Reescrever "mais limpo" quebra a identidade da plataforma.
   - **Tokens semânticos, claro e escuro.** Nada de cor fixa; toda tela conferida nos dois temas.
   - **Troca visual não muda comportamento.** Validação, texto, ordem dos campos, payload enviado à API e `data-testid` ficam iguais. Mudança de comportamento é bug.
   - **Escada da preguiça.** Precisa existir? Já existe no repo? A plataforma ou uma dependência instalada resolve? Só então escreve o mínimo.
   - **Bug: corrigir a causa.** Procura todos os lugares que usam a função e corrige uma vez, na origem.

### Provar

6. **Ponto de parada 2: a evidência.** Nenhuma PR sobe sem.
   - Prints antes (branch principal) e depois (sua branch), claro e escuro, incluindo estado de erro e desabilitado.
   - E2E da área nas duas branches. Falha que já existe na principal é pré-existente, não culpa da PR.
   - Performance da principal contra a sua branch: LCP, CLS e long tasks, medidos **em sequência, na mesma janela de tempo**. Medições separadas por horas já deram uma piora falsa de 21%.
   - Tudo registrado num `evidencias-<card>.md`, no card e no corpo da PR.
7. **Validação e docs.** Validações do time só nos pacotes tocados. Se o time exige documentação para mudança visível, ela entra na mesma PR.
8. **Revisão independente.** Um revisor separado (um subagente ou outra sessão no papel de revisor) olha só o diff, procurando bug. Se houver ajuste depois, roda de novo: a segunda rodada já pegou efeito colateral da correção da primeira.

### Entregar

9. **Commit e PR só quando você pede.** PR no padrão do time, card movido para "em revisão" com o link, pedido de revisão no formato do time.
10. **Depois de aberta.** Apontamentos do bot de revisão: o Claude corrige o que é do escopo e responde na thread. Comentário de pessoa: a conversa é sua; o Claude traz o contexto técnico de cada ponto quando você pede e aplica o que for combinado.

## Aprendizados

O método não nasceu pronto. Cada regra dele veio de algo que deu errado ou que funcionou melhor do que o esperado.

1. **Antes e depois é o entregável.** Sem o comparativo, um trabalho de correção passa despercebido: quem revisa não vê o que mudou, e quem usa nunca soube do problema. Por isso a evidência é um ponto de parada, e não um anexo.
2. **O placar fica no código, não em planilha.** Um script conta, a cada merge, quantos usos do componente antigo ainda existem, e uma regra de lint impede usos novos. Sem a trava, cinco arquivos novos com o componente antigo apareceram em quatro dias.
3. **Medir em sequência, na mesma janela.** Uma rodada de performance feita com horas de intervalo mostrou uma piora de 21% que não existia. Medindo as duas branches uma depois da outra, a diferença sumiu.
3. **Trocar componente é auditoria.** Os bugs mais sérios estavam em telas que ninguém tinha pedido para olhar. Abrir cada tela para trocar o componente revela o que já estava quebrado em volta.
4. **A IA executa; o critério de design decide.** A IA reescreveu um conjunto de abas para deixá-las "mais limpas" e quebrou a identidade da plataforma. Isso virou regra: não reconstruir o que já existe, e reusar o componente da tela de referência.
5. **Revisão independente pega o que o autor não vê.** Uma segunda sessão, olhando só o diff, encontrou um bug que já estava em produção. Desde então, a revisão roda de novo sempre que há ajuste depois dela.
6. **Medir antes de prometer, uma área por PR.** O número vem antes do compromisso. E cada PR mexe numa área só, para poder voltar atrás sem desfazer o resto.
7. **Erro corrigido vira memória.** Quando o Claude erra algo que não pode se repetir, a correção vai para a memória do projeto, com o porquê.

## Evidência

O comparativo é sempre a mesma grade: antes à esquerda, depois à direita; claro em cima, escuro embaixo. Se a troca é invisível para quem usa (uma biblioteca de formulários, por exemplo), a evidência mostra o estado de erro: as mesmas mensagens, no mesmo lugar.

Critério de performance: LCP sem piora acima de 10%, CLS não sobe, nenhuma long task nova acima de 50 ms.

Modelo do registro:

```markdown
# Evidência · <ID> <título>

## Prints
Antes (principal) à esquerda, depois (branch) à direita; claro em cima, escuro embaixo.
- <tela>: padrão, erro, desabilitado

## E2E da área
- Principal: <x de y> · Branch: <x de y>
- Pré-existentes (já falham na principal): <teste e motivo>

## Performance (as duas em sequência, na mesma janela)
| Tela | LCP antes | LCP depois | Diferença | CLS antes | CLS depois | Long tasks novas |
|-|-|-|-|-|-|-|

## Comportamento
- Validação, textos, payload e data-testid iguais: <como foi conferido>

## Validações
- <lint, tipos, testes>: <resultado>
- Não rodou, e por quê: <...>

## Revisão independente
- Rodada 1: <achados e o que mudou>
- Rodada 2: <se houve ajuste depois>
```

## Várias PRs ao mesmo tempo: a sessão orquestradora

### O problema

Cada PR roda numa sessão e numa worktree própria, mas o **ambiente local costuma ser um só**: portas fixas, um banco. Só uma worktree fica no ar por vez, e toda PR precisa dele para prints, E2E e performance. Trocar o ambiente à mão, PR por PR, não escala: cada troca depende de alguém disponível naquela hora e as PRs ficam esperando. A solução é dar o ambiente para uma sessão só, a **orquestradora**, que decide quem usa e faz a troca sozinha.

### O que ela faz e o que não faz

| Faz | Não faz |
|-|-|
| É a única dona do ambiente: sobe, troca e para | Não escreve o código das PRs |
| Mantém a fila de quem vai usar o ambiente | Não decide visual nem produto |
| Confere a carga da máquina antes de subir algo pesado | Não faz commit nem PR pelas outras sessões |
| Mantém o `STATUS.md`, o quadro de todas as PRs | Não conversa com quem revisa pelas PRs |
| Avisa as PRs que dependem umas das outras | |
| Prepara o card e o prompt da próxima PR | |

Decisões de design, commit e PR continuam indo direto para você.

### Montagem, uma vez por frente

1. **Pasta de trabalho fora do repo** com `COMO-TRABALHAR.md` (regras que toda sessão lê), o mapa da frente, `STATUS.md`, os `PROMPT-<card>.md`, as evidências e os scripts. Nada disso entra no repo.
2. **Sessão orquestradora** aberta na pasta principal do repo (ela não precisa de worktree), com um nome fácil de achar e fixada no topo.
3. **Um comando para trocar o ambiente**, por exemplo `subir-ambiente pr-14`: derruba o que estiver no ar e sobe a cópia indicada.
3. **Um atalho por worktree.** As worktrees que o app cria ficam numa pasta escondida (`.claude/worktrees/`); cada sessão de PR cria um atalho com o nome do card, e o comando de subir usa esse nome.
4. **Processos extras.** Se o ambiente tem processos que não sobem sozinhos, o script recebe os nomes deles como argumentos.
5. **Máquina acordada**, senão o ambiente cai no meio de um E2E.

### Organização no app

- **Orquestradora fixada no topo** da barra lateral.
- **Um grupo por frente**, com a orquestradora e todas as sessões de PR dentro.
- **Toda sessão com o nome do card**, com o número da PR na frente para mostrar a ordem.
- **Sessão entregue sai da frente**: concluída e, com o seu ok, arquivada.

A própria orquestradora faz isso pelas ferramentas do app, desde que esteja no prompt dela.

### A troca do ambiente

1. **A sessão de PR pede a vez** em uma linha: card, atalho, processos extras e o que vai rodar.
2. **Antes de pedir, ela já deixou a worktree pronta.** Sem setup o ambiente sobe quebrado e a vez é desperdiçada.
3. **A orquestradora confere** quem está com o ambiente, a fila e a carga da máquina.
3. **Sobe** numa aba do terminal do app, com o comando do time.
4. **Confere de onde os processos saem** antes de liberar (`ps`). Print tirado do servidor errado é trabalho jogado fora.
5. **Avisa a sessão e você** em uma linha, e atualiza o `STATUS.md`.
6. **A sessão devolve** quando termina ("ambiente livre"), e a fila anda.

### Cuidados

- **Um ambiente por vez, sempre.** Subir um pode derrubar qualquer servidor extra, inclusive o da branch principal usado nos prints de "antes". Suba esse depois.
- **Nada pesado com o ambiente no ar.** Checagem de tipos global e builds grandes sobrecarregam a máquina.
- **Infraestrutura é uma só.** Não suba banco e filas de dentro de uma worktree: isso pode criar um banco novo e vazio.
- **Duas PRs andando no máximo**: uma constrói, outra prova e documenta. Mais que isso só gera fila e conflito com a branch principal.
- **Avise o time antes de mexer numa área**, principalmente quem está mudando as mesmas telas.

### Como as sessões conversam

- Cada sessão de PR tem, no prompt, uma seção **Comunicação** com o nome da orquestradora e a regra: a cada ponto de parada, bloqueio ou fim de etapa, mandar uma linha de status para ela.
- A orquestradora não fica perguntando: as sessões reportam. Ela junta tudo no `STATUS.md`.
- Quando uma PR mergeia, a orquestradora avisa as seguintes do que muda para elas.

## Memória: corrigir uma vez só

O Claude Code tem memória por projeto. Quando ele erra algo que você não quer ver de novo, diga "lembra disso" e explique o porquê. Exemplos que valem para quase todo time:

- nunca commitar ou abrir PR sem pedido;
- agir como dev sênior;
- design system primeiro, sem reconstruir componente da plataforma;
- tudo funcionando no claro e no escuro;
- nada de build pesado com o ambiente no ar.

Com o tempo, o processo fica nas memórias e nos arquivos de regras, e os prompts ficam curtos.

## Armadilhas conhecidas

| O que acontece | Como evitar |
|-|-|
| Tela com tema inesperado: o ambiente estava rodando de uma branch desatualizada | Worktree nova da principal por card; conferir de onde o ambiente roda antes de tirar print |
| Worktree nova com dezenas de erros de "módulo não encontrado" | Rodar o setup (install e build das bibliotecas internas) antes de validar |
| Um arquivo regerado pelo servidor local entrou na PR | Stage só dos arquivos do escopo; conferir o diff antes do push |
| Checagem global com o ambiente no ar sobrecarrega a máquina | Validar só os pacotes tocados; o que é pesado roda com o ambiente parado |
| Frontend escrito para um endpoint que o backend ainda não entregou | Confirmar no contrato ou nos tipos gerados que ele existe antes de começar |
| Componente reescrito do zero fugiu da identidade visual | Reusar o componente da tela de referência |
| Performance medida em horários diferentes deu piora falsa | As duas branches em sequência, na mesma janela de tempo |
| Troca manual do ambiente vira fila de espera | A orquestradora assume a troca |

## Como começar: dois caminhos

### Caminho A: versão mínima

Uma PR, você conduz a sessão. Não precisa de orquestração, pasta de evidência nem scripts.

1. Instale a [skill](#a-skill) e preencha a configuração do time.
2. Escolha um card pequeno e visual. Um bug de tema escuro numa tela só é perfeito.
3. Abra uma sessão nova no app, na pasta do repositório, com o nome do card.
4. Cole o [prompt de entrada](#modelo-de-prompt-de-entrada) preenchido.
5. Aprove o plano antes de qualquer edição.
6. Acompanhe pelo navegador do app, no claro e no escuro.
7. Aprove a evidência: prints antes e depois, E2E e revisão independente.
8. Só então peça commit e PR.

### Caminho B: versão automatizada

Para quando a entrega é maior que uma PR: uma área inteira, uma migração, um conjunto de telas. Você conversa com **uma sessão só**, a orquestradora, e ela faz o resto.

**O que você entrega no início:** o objetivo da frente, o card pai, as referências (Figma, telas que já têm o padrão), o que fica de fora e quem precisa ser avisado.

**O que ela faz sozinha:**

1. Mapeia as telas e componentes afetados e escreve o mapa (inventário, ordem das PRs, riscos, dependências).
2. Quebra em PRs pequenas e cria os sub-cards.
3. Escreve o `PROMPT-<card>.md` de cada PR, já com o que as anteriores aprenderam.
4. Abre a sessão de cada PR, cada uma na sua worktree. No máximo duas andando ao mesmo tempo.
5. Organiza a barra lateral.
6. Controla o ambiente: fila, troca, conferência e devolução.
7. Junta o status no `STATUS.md` e te resume só o que espera de você.
8. Quando uma PR mergeia, avisa as seguintes e libera a próxima da fila.

**Onde você entra:**

| Momento | O que você faz |
|-|-|
| Mapa e divisão das PRs | Aprova ou ajusta a ordem e o tamanho |
| Plano de cada PR | Aprova antes de editar |
| Decisão visual ou de produto no caminho | Decide |
| Evidência de cada PR | Aprova |
| Commit e PR | Diz "pode commitar e abrir" |
| Comentário de quem revisa | Conduz a conversa e decide o que muda |

Faça o Caminho A pelo menos uma vez antes, para conhecer as etapas que a orquestradora vai automatizar.

## Modelo de prompt de entrada

```text
Card: <ID> <título do card> (<link do card>)
Renomeie esta sessão para o nome do card.

Objetivo: <o que muda para quem usa, em 1 ou 2 frases>
Referência visual: <link do Figma e/ou tela que já tem o padrão>
Fora do escopo: <o que não mexer>
Branch: <padrão de branch do time>

Como trabalhar:
- Aja como dev sênior: decida o que é técnico e reversível; me pergunte só produto, visual, algo que envolva outra pessoa ou algo irreversível.
- Responda em português.
- Worktree nova a partir da <branch principal> atualizada; rode <setup da worktree>.
- <Design system> primeiro. Se a tela de referência já tem o componente, reuse o mesmo e ajuste só por props e classes.
- Tokens semânticos; a tela tem que funcionar no claro e no escuro.
- Sem mudar comportamento: validações, textos, data-testid e payload iguais.

Pontos de parada:
1. Antes de editar, me mande o plano (arquivos, componentes, riscos).
2. Antes de commit, me mostre prints antes e depois, claro e escuro, o resultado do E2E da área e das validações, e rode uma revisão independente do diff.
Commit e PR só quando eu pedir, no padrão: <padrão de PR>.
```

## Modelo de prompt da sessão orquestradora

```text
Você é a sessão orquestradora da frente <nome da frente> (card pai <ID>).
Renomeie esta sessão para "<ID> orquestração".
Responda em português. Aja como dev sênior: decida o que é técnico e reversível;
me pergunte só produto, visual, algo que envolva outra pessoa ou algo irreversível.

Frente:
- Objetivo: <o que muda para quem usa>
- Referências: <Figma, telas que já têm o padrão>
- Fora do escopo: <o que não mexer>
- Avisar antes de mexer: <quem está nas mesmas telas>
- Pasta de trabalho (fora do repo): <caminho>

1. Mapa e divisão
- Levante no código (branch principal atualizada) as telas e componentes afetados.
- Escreva <pasta>/mapa.md: inventário, ordem das PRs, riscos, dependências.
- Proponha a divisão em PRs pequenas e PARE para eu aprovar.
- Aprovada: crie os sub-cards (título com uns 40 caracteres), um <pasta>/PROMPT-<card>.md
  por PR (com uma seção Comunicação com o seu nome) e um <pasta>/COMO-TRABALHAR.md
  com as regras comuns.

2. Sessões de PR e organização no app
- Abra uma sessão por PR, com o nome do card, numa worktree própria, mandando ler
  o PROMPT dela. No máximo duas PRs andando ao mesmo tempo.
- Fixe esta sessão no topo da barra lateral; crie o grupo "<ID> <nome da frente>"
  e mova para ele esta sessão e cada sessão de PR assim que for criada.
  PR mergeada: marque a sessão como concluída e me pergunte se pode arquivar.

3. Ambiente (você é a única dona dele)
- Sessões pedem a vez por mensagem. Antes de subir, confira quem está com o
  ambiente, a fila e o uptime; se a sessão não fez o setup, devolva o pedido.
- Suba numa aba do terminal do app com <comando de subir o ambiente>, confira com
  ps que os processos saem da worktree certa e atualize o banco local se estiver
  atrás. Avise a sessão e me avise em uma linha.
- Um ambiente por vez; nada pesado com ele no ar; nunca suba banco e filas de
  dentro de uma worktree.

4. Acompanhamento
- Mantenha <pasta>/STATUS.md: tabela das PRs (card, sessão, etapa, o que espera
  de mim, próximo passo), com quem está o ambiente e um registro datado.
- Quando uma PR mergear, avise as seguintes do que muda para elas e libere a
  próxima da fila.
- Ao fim de cada etapa, me mande um resumo curto só com o que depende de mim.

Você não escreve o código das PRs, não decide visual e não faz commit nem PR por elas.
```

## A skill

A skill reúne este processo num arquivo só, escrito para o Claude ler. Salve em `~/.claude/skills/processo-frontend/SKILL.md`, preencha a seção "Configuração do time" e abra uma sessão nova. Depois disso, o prompt de entrada só precisa do card, do objetivo e da referência.

```bash
mkdir -p ~/.claude/skills/processo-frontend && curl -fsSL https://eltoncarvalho.com.br/processo/SKILL.md -o ~/.claude/skills/processo-frontend/SKILL.md
```

---

Elton Carvalho · novembro de 2026
