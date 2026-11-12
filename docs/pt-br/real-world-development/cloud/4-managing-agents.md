---
title: "Exercício 4 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Nas últimas lições, você pediu ao agente de nuvem do Copilot que realizasse três tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Embora o agente trabalhe de forma assíncrona e autônoma, é importante monitorar essas tarefas.

Há várias ferramentas para gerenciar as tarefas atribuídas ao agente, incluindo a [página de agentes][agents-page] no GitHub.com. Nesse painel central, você pode ver todas as tarefas com pull requests (PRs) abertos, explorar as operações realizadas e orientar uma sessão em andamento.

Nesta lição, você vai:

- explorar a página de agentes para monitorar as tarefas do agente de nuvem.
- orientar uma sessão em andamento para solicitar funcionalidades adicionais.

## Cenário

Depois de atribuir ao agente a criação de um modo de alto contraste, a equipe decidiu que seria um bom momento para adicionar também um modo claro. Como o trabalho já envolve atualizar o estilo do site e adicionar controles para alternar modos, faz sentido incluir essa funcionalidade. Você orientará o agente para que ele implemente também o modo claro.

## Revisar as tarefas do agente de nuvem

Confira o status das tarefas atribuídas ao agente de nuvem do Copilot.

1. Acesse a [página de agentes do Copilot](https://github.com/copilot/agents).
2. Observe as tarefas listadas no painel principal e no painel esquerdo. Entre elas, você deverá encontrar:
   - atualização da documentação da base de código.
   - geração de APIs para modificar jogos.
   - adição de um modo de alto contraste ao site.
3. Selecione uma tarefa em andamento e revise as operações realizadas pelo Copilot, que podem incluir:
   - obter o código do repositório.
   - configurar o ambiente de trabalho do Copilot.
   - configurar servidores do Model Context Protocol (MCP).
   - executar várias etapas para concluir a tarefa.

> [!NOTE]
> As etapas listadas variam conforme o estado do trabalho e a abordagem adotada pelo Copilot.

4. Observe também o painel de pull requests à direita, que mostra o PR e os arquivos alterados.

## Orientar o agente de nuvem

Agora que você conhece as tarefas em andamento, peça ao Copilot que adicione o controle do modo claro enquanto trabalha no modo de alto contraste.

1. Selecione a sessão referente ao modo de alto contraste. O título exato varia conforme o nome usado pelo Copilot e o estado atual do trabalho.

   ![Sessão de acessibilidade no painel de agentes](../../../_images/ex6-accessibility-session.png)

2. Acompanhe a sessão por alguns minutos, até que a configuração seja concluída e o trabalho comece.
3. Na caixa de diálogo **Steer active session while Copilot is working**, envie este prompt:

   ```plaintext
   Enquanto trabalhamos no modo de alto contraste, vamos adicionar também um modo claro. Deve haver um controle para esse modo, para que as pessoas usuárias possam escolher a exibição desejada.
   ```

   ![Captura de tela da tarefa do agente de nuvem na página de agentes, com a caixa de diálogo de orientação da sessão ativa destacada](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pressione <kbd>Enter</kbd> para enviar o prompt.
5. Observe como o Copilot confirma o recebimento do pedido e o incorpora ao fluxo de trabalho.

## Deixar o Copilot trabalhar

O Copilot incorporará o novo pedido ao trabalho depois de concluir a etapa que estava executando quando você enviou a mensagem.

Isso levará alguns minutos. Aproveite para fazer uma pausa e refletir sobre o que aprendeu até aqui.

## Resumo e próximos passos

Você explorou a página de agentes do Copilot, o painel central para monitorar e orientar tarefas do agente de nuvem. Nela, é possível acompanhar tarefas em andamento e concluídas, revisar o trabalho e redirecionar uma sessão ativa para ajustar o escopo ou fornecer orientações adicionais.

Nesta lição, você:

- explorou o painel de agentes para monitorar tarefas do agente de nuvem.
- redirecionou uma sessão em andamento para solicitar funcionalidades adicionais.

Enquanto o Copilot conclui as alterações de acessibilidade, você [iterará sobre os pull requests criados pelo Copilot][next-lesson].

## Recursos

- [Página de agentes do Copilot][agents-page]
- [Sobre agentes personalizados][custom-agents]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
