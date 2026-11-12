---
title: "Exercício 5 - Monitorar e gerenciar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Agentes personalizados][previous-lesson] |
|:--|

No modo de agente, o GitHub Copilot trabalha de forma autônoma: explora a base de código, propõe alterações, edita arquivos e executa comandos. Como o trabalho acontece na sua máquina em tempo real, o Copilot Chat no VS Code mostra cada chamada de ferramenta e edição de arquivo. Você pode revisar diferenças, aceitar ou rejeitar mudanças e orientar a conversa com prompts complementares.

Neste exercício, você vai:

- acompanhar o trabalho do agente de acessibilidade em tempo real.
- revisar e aceitar as alterações propostas.
- orientar o agente durante a sessão para adicionar um controle do modo claro junto ao modo de alto contraste.

## Cenário

O agente personalizado de acessibilidade usado no [Exercício 4][previous-lesson] está implementando o modo de alto contraste. Enquanto o trabalho acontece, a equipe de design solicita também um modo claro para pessoas que consideram o tema padrão escuro demais. Em vez de começar uma conversa nova, você ampliará a sessão existente.

## Acompanhar o progresso do Copilot

O Copilot Chat mostra as etapas executadas pelo agente: arquivos explorados, comandos executados e alterações propostas. Cada edição aparece com uma diferença e os controles **Keep** e **Undo**.

1. Volte à visualização Copilot Chat do Exercício 4.
2. Acompanhe as chamadas de ferramentas, leituras e edições de arquivos e os comandos de terminal solicitados.
3. Quando uma edição aparecer, selecione **Keep** para aceitá-la ou **Undo** para revertê-la e permitir outra tentativa.
4. Abra **Files changed**, na parte superior do chat, para ver todos os arquivos alterados.

> [!NOTE]
> Se uma chamada de ferramenta solicitar permissão, por exemplo, para executar um comando de terminal, o agente aguardará sua resposta em **Allow**. Aprove apenas comandos que você considera seguros.

5. Aguarde o agente concluir o modo de alto contraste. Ele apresentará uma mensagem final com o resumo das alterações.

## Orientar o agente para adicionar o modo claro

Agora, amplie a mesma conversa para adicionar um controle do modo claro. Como você continuará na mesma sessão, o agente manterá o contexto dos componentes, dos estilos e do padrão de armazenamento local que já implementou.

1. Na caixa de entrada do Copilot Chat, envie este prompt:

   ```plaintext
   Bom trabalho! Agora, adicione um controle do modo claro ao lado do controle de alto contraste. Siga o mesmo padrão: persista a preferência no armazenamento local e disponibilize o controle na mesma área da interface. As pessoas usuárias devem poder ativar o alto contraste e o modo claro de forma independente.
   ```

2. O agente revisará as alterações existentes e proporá mudanças para adicionar o modo claro.
3. Revise cada nova edição e selecione **Keep** ou **Undo**.
4. Se o agente seguir uma direção indesejada, selecione **Stop** ao lado da caixa de entrada e envie uma mensagem complementar para esclarecer o pedido.

> [!TIP]
> É mais rápido orientar uma sessão em andamento do que começar de novo. Peça ajustes, como simplificar o CSS usando variáveis, corrigir o rumo sem adicionar um terceiro controle ou ampliar o escopo para incluir atalhos de teclado.

## Revisar as alterações

Antes de fazer commit, revise o conjunto de arquivos alterados pelo agente.

1. Abra a visualização **Source Control** no VS Code.
2. Revise a lista de arquivos alterados, que deve incluir componentes Astro, estilos e testes relacionados.
3. Abra alguns arquivos e examine as diferenças. Confirme se as práticas de acessibilidade do agente — atributos de Accessible Rich Internet Applications (ARIA), navegação por teclado, HyperText Markup Language (HTML) semântico e persistência no armazenamento local — estão presentes.
4. Quando estiver satisfeito, prepare e faça commit das alterações no painel Source Control. Você as publicará na [próxima lição][next-lesson].

## Resumo e próximos passos

Você usou o modo de agente do Copilot Chat para acompanhar e orientar uma sessão em andamento: revisou cada alteração, aceitou ou rejeitou mudanças e enviou prompts complementares para ampliar o trabalho sem perder o contexto.

Nesta lição, você:

- acompanhou o trabalho do agente em tempo real.
- aceitou ou rejeitou alterações individuais.
- orientou a sessão com prompts complementares.

Na [próxima lição][next-lesson], você publicará o trabalho de acessibilidade em um pull request e revisará as alterações do agente personalizado.

## Recursos

- [Copilot Chat no VS Code][copilot-chat-vscode]
- [Usar o modo de agente][agent-mode]

---

| [← Lição anterior: Agentes personalizados][previous-lesson] | [Próxima lição: Iterar sobre o trabalho do Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
