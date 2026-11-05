---
name: texto-de-interface
description: Escreve e revisa o texto da interface em português do Brasil — botões, títulos, rótulos, mensagens de erro, estados vazios, confirmações, avisos, onboarding e notificações — com voz clara, ativa e consistente. Use ao criar ou revisar qualquer tela, componente ou fluxo com texto, ao traduzir uma interface do inglês, e quando a pessoa disser "melhora o texto", "o botão está estranho", "a mensagem de erro está ruim", "escreve o microcopy", "está robótico" ou "deixa mais humano".
---

# Texto de interface

Versão 1.0 · novembro de 2026 · por Elton Carvalho · eltoncarvalho.com.br/skills

Na interface, texto é design: ele diz o que cada coisa é, o que vai acontecer e o que fazer quando algo dá errado. Texto ruim deixa uma tela bonita confusa; texto bom some e a pessoa só segue em frente. Esta skill escreve em português do Brasil, do jeito que as pessoas falam.

## Os princípios

1. **Claro antes de criativo.** A pessoa precisa entender de primeira. Trocadilho só onde não atrapalha (um estado vazio, uma celebração), nunca em botão, erro ou formulário.
2. **Fale de você para a pessoa.** Trate por "você" (ou sem pronome), em tom de conversa. Evite "o usuário", "favor", "prezado" e o imperativo seco de sistema ("Insira os dados").
3. **Nomeie pelo que a pessoa reconhece**, não pelo que o sistema é por dentro: "Notificações", não "Configuração de webhooks"; "Pagamento recusado", não "Erro 402".
4. **Voz ativa e verbo no começo.** "Salvamos suas alterações", não "As alterações foram salvas com sucesso".
5. **Cada texto faz um trabalho.** Título diz onde a pessoa está, rótulo diz o que é, botão diz o que acontece, ajuda diz o que fazer. Corte o resto.
6. **Mesma ação, mesma palavra, do começo ao fim.** Se o botão diz "Publicar", o aviso diz "Publicado" e o menu diz "Publicar", não "Enviar" nem "Postar".

## Padrões por peça

**Botões**
- Verbo + objeto quando houver dúvida: "Salvar rascunho", "Agendar visita", "Excluir projeto". Só o verbo quando o contexto é óbvio: "Salvar".
- Nada de "OK", "Enviar" ou "Clique aqui" quando dá para dizer a ação.
- Ação destrutiva repete o objeto: "Excluir 3 arquivos", não "Confirmar".
- Até ~3 palavras; primeira letra maiúscula e o resto minúsculo.

**Títulos e rótulos**
- Frase com só a primeira letra maiúscula: "Dados de pagamento", não "Dados De Pagamento" nem tudo em maiúsculas.
- Sem ponto final em títulos, rótulos e botões. Com ponto final em frases completas de ajuda.
- Rótulo de campo é substantivo curto ("E-mail", "Data de nascimento"); a ajuda embaixo diz o formato ou o porquê ("Usamos para enviar o recibo").

**Mensagens de erro**
Diga o que aconteceu e o que fazer, sem culpar a pessoa e sem pedir desculpas em excesso.
- Ruim: "Erro! Dados inválidos." · Bom: "Esse CPF tem 11 números. Confira e tente de novo."
- Ruim: "Ocorreu um erro inesperado." · Bom: "Não conseguimos salvar agora. Suas alterações estão guardadas aqui; tente de novo em alguns segundos."
- Erro de campo fica junto ao campo e fala só daquele campo.

**Estados vazios**
Um título que diz o que estaria ali, uma linha que diz como começar e um botão com a ação.
- "Nenhum projeto ainda" · "Crie o primeiro e convide seu time quando quiser." · [Criar projeto]
- Vazio de busca é diferente de vazio de início: "Nada encontrado para "fatura março". Tente outra palavra ou limpe os filtros."

**Confirmações e avisos (toasts)**
- Curto, no passado, com o objeto: "Projeto excluído". Se der para desfazer, ofereça: "Projeto excluído · Desfazer".
- Diálogo de confirmação só para o que não tem volta. Título em forma de pergunta com o objeto ("Excluir o projeto Lua?"), uma linha com a consequência e botões com as ações ("Excluir projeto" / "Cancelar").

**Carregando e progresso**
- Diga o que está acontecendo quando demora: "Gerando o relatório…" em vez de só um spinner.
- Use reticências (…) para ações em andamento e o caractere de reticências, não três pontos.

**Números, datas e unidades (pt-BR)**
- Decimal com vírgula e milhar com ponto: 1.234,56. Moeda: R$ 49,90 (com espaço).
- Datas: 5 de novembro de 2026, ou 05/11/2026 em tabelas. Horas: 14h30.
- Espaço entre número e unidade: 12 MB, 30 min. Porcentagem junto: 15%.

## Traduzindo do inglês

- Não traduza palavra por palavra: "Get started" vira "Começar", "Learn more" vira algo específico ("Ver como funciona"), "You're all set" vira "Tudo pronto".
- Evite anglicismos quando existe palavra comum: "Entrar" (não "Logar"), "Enviar" (não "Submeter"), "Configurações" (não "Settings").
- Termos que o público já usa em inglês (app, link, e-mail, login como substantivo) podem ficar.
- Português é ~20–30% mais longo: confira se cabe no botão e no celular antes de entregar.

## Como revisar

Ao revisar uma tela, entregue uma tabela curta:

| Onde | Hoje | Proposta | Por quê |
|---|---|---|---|

Mude direto o que é técnico e óbvio (pontuação, maiúsculas, consistência de termos). Traga para a pessoa o que muda o tom da marca ou o significado.

## Checklist

- [ ] Dá para entender cada texto de primeira, sem contexto extra?
- [ ] Botões dizem a ação; destrutivos repetem o objeto?
- [ ] A mesma ação tem o mesmo nome em todo o fluxo?
- [ ] Erros dizem o que houve e o que fazer, sem culpar?
- [ ] Estados vazios têm título, uma linha e uma ação?
- [ ] Maiúscula só na primeira letra; sem ponto em botões e títulos?
- [ ] Números, datas e moeda no padrão brasileiro?
- [ ] Cabe no celular?
