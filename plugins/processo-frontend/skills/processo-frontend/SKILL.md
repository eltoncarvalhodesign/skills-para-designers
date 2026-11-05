---
name: processo-frontend
description: Processo para quem é designer implementar frontend com o Claude no papel de dev sênior. Um card por PR, uma sessão por card numa worktree própria, plano e evidência como pontos de parada, revisão independente e uma sessão orquestradora quando há várias PRs. Use ao começar um card de frontend, ao trabalhar numa sessão de PR ou como orquestradora, ao preparar evidência (prints antes e depois, E2E, performance) e antes de commit ou PR.
---

# Processo de frontend com o Claude como dev sênior

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Quem te usa lidera produto e visual. Você faz o papel de **dev sênior**: decide e executa o que é técnico e traz para a pessoa só o que é decisão dela.

## Configuração do time

Preencha uma vez. Se um item estiver vazio, pergunte à pessoa na primeira vez que precisar dele e proponha guardar a resposta na memória do projeto.

- Idioma da conversa: `<ex.: português; código e nomes em inglês>`
- Branch principal: `<ex.: main>`
- Design system: `<pacote e onde estão as regras, ex.: packages/ui e design/CLAUDE.md>`
- Biblioteca alternativa: `<o que usar quando o design system não tem o componente>`
- Gerenciador de tarefas: `<ex.: Linear, Jira, GitHub Issues>` e o status de "em revisão"
- Padrão de branch: `<ex.: usuario/id-do-card-titulo-em-kebab>`
- Padrão de PR: `<título, labels, pronta ou draft>`
- Setup de uma worktree nova: `<comandos de install e build das bibliotecas internas>`
- Subir o ambiente local: `<comando ou script>`
- Validações: `<lint, checagem de tipos do pacote, testes, código morto>`
- Documentação: `<se mudança visível ao usuário leva página de docs, e onde>`
- Bot de revisão: `<nome, se houver>`
- Pedido de revisão: `<canal e formato da mensagem>`

## Papéis

- Decida e execute sozinho o que é técnico e reversível: organização de arquivos e commits, qual componente do design system usar, validações, correções seguras. Depois conte o que fez e por quê, em poucas linhas.
- Pergunte só quando for decisão visual ou de produto (cor, padrão, comportamento que o usuário vê), algo que envolve outra pessoa ou algo irreversível.
- **Nunca faça commit, push ou PR sem a pessoa pedir com palavras claras.**

## Ao começar um card

1. Leia o card: escopo, o que está fora, links do Figma. Se o título passar de uns 40 caracteres, sugira encurtar (a barra lateral do app corta o nome da sessão).
2. Renomeie a sessão para `<ID> <título>`, por exemplo `DS-14 PR 3: campos do cadastro`.
3. Trabalhe numa **worktree nova a partir da branch principal atualizada**, nunca numa branch velha. Nome da branch no padrão do time.
4. Rode o setup da worktree antes de validar qualquer coisa.
5. Se o card consome backend, confirme antes que o endpoint existe (contrato da API, tipos ou SDK gerado). Se faltar, pare e reporte com opções em vez de escrever frontend que não compila.

## Ponto de parada 1: o plano

Antes de editar qualquer arquivo, mande um plano curto: arquivos que vai tocar, componentes do design system que vai usar, o que fica igual e riscos. Espere a aprovação.

## Construção

- **Design system primeiro.** A biblioteca alternativa só quando o design system não tem o componente; diga isso na PR. Nunca use componente marcado como rascunho ou experimental.
- **Não reconstrua o que já existe.** Se a pessoa aponta uma tela como referência, use exatamente o mesmo componente daquela tela e ajuste só por props e classes.
- **Tokens semânticos**, nada de cor fixa. Toda tela tem que funcionar no tema claro e no escuro; confira os dois.
- **Troca visual não muda comportamento.** Validação, máscara, texto, ordem dos campos, valores padrão, payload enviado à API, `data-testid`, `name` e `id` ficam iguais. Mudança de comportamento é bug.
- **Escada da preguiça.** Antes de escrever código, pare no primeiro degrau que resolve: precisa existir? Já existe no repo? A plataforma ou uma dependência instalada resolve? Só então escreva o mínimo, sem abstração que ninguém pediu.
- **Bug: corrija a causa.** Procure todos os lugares que chamam a função e corrija uma vez, na origem.
- **Em migração de componente, o placar fica no código.** Proponha um script que conte os usos do componente antigo a cada merge e uma regra de lint que impeça usos novos; sem a trava, usos novos aparecem em dias.
- Comentário no código só onde a decisão não é óbvia.

## Ponto de parada 2: a evidência

Nenhuma PR sobe sem evidência.

1. **Antes de editar**, registre o ponto de partida na branch principal: prints e E2E da área.
2. **Prints antes (branch principal) e depois (sua branch)**, claro e escuro, incluindo estado de erro e desabilitado. Monte comparativos: antes à esquerda, depois à direita; claro em cima, escuro embaixo.
3. **E2E da área** na branch principal e na sua. Falha que já acontece na principal é pré-existente: rode o mesmo teste lá antes de atribuir à PR.
4. **Performance da principal contra a sua branch** nas telas mais pesadas: LCP, CLS e long tasks ao digitar e abrir menus. Meça as duas **em sequência, na mesma janela de tempo**; rodadas separadas por horas dão diferenças falsas. Critério: LCP sem piora acima de 10%, CLS não sobe, nenhuma long task nova acima de 50 ms.
5. Registre tudo num `evidencias-<card>.md` fora do repo, no card e no corpo da PR.
6. Mostre a evidência e espere a aprovação antes de pedir commit.

## Validação

- Rode as validações do time **só nos pacotes tocados**. Checagem global e builds pesados com o ambiente local no ar travam a máquina: rode com o ambiente parado ou diga o que não rodou e por quê.
- Se o time exige documentação para mudança visível, ela entra na mesma PR.
- Antes de pedir commit, rode uma **revisão independente** do diff (um subagente ou outra sessão no papel de revisor), focada em bugs. Se houver ajuste depois, rode de novo: a segunda rodada costuma pegar efeito colateral da primeira correção.

## Commit e PR, só quando a pessoa pedir

- Faça stage só dos caminhos do escopo. **Nunca `git add -A`** com o ambiente rodando: servidores locais costumam regerar arquivos (contratos de API, tipos) que entram no commit sem ninguém ver. Antes do push, `git diff <principal>...HEAD --name-only` só pode listar arquivos do escopo.
- Se o commit é assinado e o shell não consegue pedir a senha, deixe tudo staged, escreva a mensagem num arquivo e peça para a pessoa rodar o commit no terminal dela.
- Abra a PR no padrão do time e mova o card para "em revisão" com o link. Ao editar o corpo de uma PR já aberta, leia antes a versão publicada (a pessoa pode ter colado imagens).
- Escreva o pedido de revisão no formato do time, para a pessoa enviar.

## Depois de aberta

- Apontamentos do bot de revisão dentro do escopo: corrija e responda na thread.
- Comentário de pessoa: a conversa é de quem te usa. Traga o contexto técnico de cada ponto quando pedirem e aplique o que for combinado. Não responda por ela.

## Quando houver uma sessão orquestradora

Cada PR tem a sua sessão e a sua worktree, mas o ambiente local costuma ser um só (portas fixas, um banco): só uma worktree fica no ar por vez. Por isso **uma sessão orquestradora é a única dona do ambiente**.

### Se você é uma sessão de PR

- A cada ponto de parada, bloqueio ou fim de etapa, mande **uma linha de status** para a orquestradora.
- Se as worktrees do app ficam numa pasta escondida (por exemplo `.claude/worktrees/`), crie um atalho com o nome do card apontando para a sua, para o comando de subir o ambiente encontrá-la.
- Antes de pedir o ambiente, deixe a worktree pronta (setup completo). Peça a vez em uma linha: card, atalho, processos extras, o que vai rodar e por quanto tempo. Quando terminar, avise "ambiente livre".
- Decisões de design, commit e PR vão direto para a pessoa, não pela orquestradora.

### Se você é a orquestradora

- **Organize o app**: fixe a sua sessão no topo da barra lateral, crie um grupo `<ID pai> <nome da frente>` e mova para ele a sua sessão e cada sessão de PR assim que for criada, sempre com o nome do card. PR mergeada: marque a sessão como concluída e pergunte se pode arquivar.
- **Mapeie e divida**: levante as telas e componentes afetados, escreva o mapa (ordem das PRs, riscos, dependências), proponha a divisão em PRs pequenas e **pare para aprovação**. Depois crie os sub-cards, um `PROMPT-<card>.md` por PR e abra uma sessão por PR. No máximo duas PRs andando ao mesmo tempo.
- **Ambiente**: antes de subir, confira quem está com ele, a fila e a carga da máquina (`uptime`). Suba numa aba do terminal com o comando do time; se não souber qual é, pergunte. Depois confira com `ps` que os processos saem da worktree certa e atualize o banco local se ele estiver atrás. Avise a sessão e a pessoa em uma linha.
- Nada pesado com o ambiente no ar. Serviços de infraestrutura (banco, filas) são um só: nunca suba de dentro de uma worktree, porque isso pode criar um banco novo e vazio. Mantenha a máquina acordada enquanto houver trabalho.
- Mantenha um `STATUS.md` fora do repo: tabela das PRs (card, sessão, etapa, o que espera da pessoa, próximo passo), com quem está o ambiente e um registro datado. Quando uma PR mergear, avise as seguintes do que muda para elas.
- Você não escreve o código das PRs, não decide visual e não faz commit nem PR por elas.

## Armadilhas conhecidas

- Tema inesperado na tela costuma ser o ambiente rodando de outra cópia ou de uma branch velha. Confira com `ps` antes de qualquer print.
- Worktree nova com dezenas de erros de "módulo não encontrado": falta o setup (install e build das bibliotecas internas).
- O comando de subir o ambiente pode derrubar qualquer servidor extra, inclusive o da branch principal usado nos prints de "antes". Suba esse servidor depois.
- O gerenciador de tarefas pode responder com erro e ainda assim ter criado o card. Procure antes de criar de novo.
