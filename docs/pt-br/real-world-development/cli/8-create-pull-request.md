---
title: "Lição 8 - Criar e mesclar o PR da funcionalidade"
description: "Revise a filtragem, as instruções, a atualização da skill, o perfil de QA e os testes; depois, crie o PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

A implementação da filtragem, as atualizações das instruções e da skill, o perfil de garantia de qualidade (QA) e os testes estão salvos em um branch. Agora, revise tudo em conjunto e abra um pull request. Você mesclou manualmente o pull request (PR) das avaliações por estrelas; desta vez, permitirá que o **Agent Merge** gerencie o processo.

> [!NOTE]
> Em geral, dividiríamos a funcionalidade, as atualizações de instruções e da skill e o agente de QA em alguns PRs. Para simplificar o workshop, mantivemos todo o fluxo de filtragem e qualidade em uma conversa e um branch, e incluiremos tudo neste PR.

Nesta lição, você vai:

- aprender o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionar toda a alteração da funcionalidade e as evidências de verificação.
- criar o PR de filtragem.
- habilitar o Agent Merge somente depois da revisão e confirmar a mesclagem do PR.

## Cenário

Durante o fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar uma funcionalidade. Agora, a Tailspin Toys quer automatizar o trabalho restante do PR, mantendo a autorização para mesclar sob controle do desenvolvedor.

## Conhecer o Agent Merge

O **Agent Merge** automatiza o trabalho restante para concluir um pull request. Quando habilitado, o Copilot resolve os impedimentos do PR — corrige verificações de integração contínua (CI) com falha, responde aos comentários de revisão e faz rebase quando necessário — e, em seguida, habilita a mesclagem automática do GitHub se as configurações do repositório permitirem.

Até agora, você selecionou **Merge pull request** manualmente. O Agent Merge pode assumir essa responsabilidade. Revise o trabalho e confirme que ele está pronto antes de habilitar o Agent Merge.

## Usar o Agent Merge para gerenciar o PR

Com todo o código pronto, revise as alterações, crie o PR e permita que o Agent Merge gerencie o restante do processo.

1. Volte ao codespace.
2. Abra a caixa de diálogo do agente digitando `/agent`.
3. Na lista de opções, selecione **Default** e pressione <kbd>Enter</kbd>.
4. Crie um novo PR com o comando `/pr create`.
5. Ative o Agent Merge com `/pr agentmerge`.
6. O Copilot acompanhará o processo de integração contínua do PR e fará a mesclagem quando tudo for aprovado.
7. Confirme se o Copilot exibe uma mensagem semelhante a "PR #14 was squash-merged successfully".

> [!IMPORTANT]
> O Agent Merge não ignora aprovações obrigatórias, proteção de branch, filas de mesclagem, configurações do repositório nem permissões ausentes. Se o processo for bloqueado, leia o motivo informado e, quando o repositório permitir, conclua manualmente a mesclagem revisada.

## Resumo e próximos passos

Você automatizou várias partes do processo de desenvolvimento: geração de código, testes e validação e, agora, o processo de pull request. Nesta lição, você:

- aprendeu o que é o Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionou toda a alteração da funcionalidade e as evidências de verificação.
- criou o PR de filtragem.
- habilitou o Agent Merge somente depois da revisão e confirmou a mesclagem do PR.

Em seguida, você [explorará outros comandos de barra úteis do Copilot CLI][next-lesson] para gerenciar contexto, modelos e compartilhamento e delegar tarefas opcionalmente à nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
