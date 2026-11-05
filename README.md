# Skills para designers

Skills de design para o [Claude Code](https://claude.com/claude-code), feitas por designer, em português. Cada uma ensina o Claude a seguir uma regra ou um processo que eu uso em projetos reais.

Vitrine com exemplos: https://eltoncarvalho.com.br/skills/

## Instalar

No Claude Code:

```
/plugin marketplace add eltoncarvalhodesign/skills-para-designers
/plugin install grade-4px@skills-para-designers
```

Troque `grade-4px` pela skill que quiser. Para atualizar depois: `/plugin marketplace update skills-para-designers`.

## As skills

| Skill | O que faz |
|---|---|
| `processo-frontend` | Designer implementa frontend com o Claude como dev sênior: um card por PR, worktree própria, plano e evidência como pontos de parada, revisão independente. Guia completo em `PROCESSO.md`. |
| `direcao-de-arte` | Assunto, tom, tipografia, cor e uma única ousadia definidos antes do código, para fugir do visual genérico de IA. |
| `acabamento` | Estados de cada componente, microinterações, curvas e durações, toque e detalhes invisíveis. |
| `temas-prontos` | Seis temas com tokens claro e escuro e contraste conferido, ou um tema novo a partir da sua marca. |
| `grade-4px` | Todo espaçamento numa grade de 4 px, com conferência antes de entregar. |
| `menos-e-mais` | Uma ideia por tela, pop-ups sem rolagem, desenho antes de gráfico, movimento simples. |
| `mobile-cara-de-app` | Celular com cara de app: bottom sheets, botões na zona do polegar, estados vazios, áreas seguras. |
| `site-leve` | Animação só em transform e opacity, o pesado carrega depois, nada roda com a aba escondida. |

Depois de instalar, a skill entra sozinha quando o assunto aparece ("o espaçamento está estranho", "no celular está quebrado"). Também dá para chamar pelo nome: `/grade-4px`.

## Versões

Cada skill tem versão própria. O que mudou fica no [CHANGELOG](CHANGELOG.md).

## Licença

MIT. Use, adapte e compartilhe. Se melhorar alguma, me conte: oi@eltoncarvalho.com.br
