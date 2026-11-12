---
title: "Exercício 5: Iterar sobre o trabalho do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

## Revisar o trabalho

Durante este laboratório, você usou o GitHub Copilot em tarefas para melhorar a experiência do usuário e adicionar funcionalidades. Pediu ao Copilot que documentasse o código, criasse uma funcionalidade de jogos relacionados para a equipe de design avaliar e implementasse recursos de acessibilidade, como controles para os modos de alto contraste e claro. Agora, revise as alterações e, se necessário, dê feedback ao Copilot.

### Cenário

A inclusão de IA generativa não muda os fundamentos de design de software e DevOps. O código gerado ainda precisa ser revisado pelo fluxo normal. Revise as sugestões do GitHub Copilot para a documentação, os jogos relacionados e a acessibilidade antes de solicitar a revisão do restante da equipe.

## Segurança e agente de nuvem do GitHub Copilot

Como o agente de nuvem executa tarefas de forma assíncrona e sem supervisão contínua, há restrições de segurança:

- O Copilot tem acesso de leitura ao repositório e acesso de escrita **somente** ao branch usado para o código.
- O agente de nuvem é executado no GitHub Actions em um ambiente separado e temporário.
- Uma pessoa precisa aprovar a execução de fluxos de trabalho do GitHub Actions.
- [O acesso a recursos externos é limitado por padrão](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluindo servidores do Model Context Protocol (MCP).

## Revisar a documentação gerada

Comece pelo primeiro pull request (PR) criado pelo agente de nuvem: o PR que adiciona documentação ao código.

> [!NOTE]
> O PR pode mostrar um aviso de que o Copilot está bloqueado por um firewall. Isso é **esperado**: por padrão, o Copilot tem acesso limitado a recursos externos, inclusive servidores MCP. Se quiser, você pode [personalizar ou desabilitar o firewall do agente de nuvem][agent-firewall].

1. Volte ao seu repositório no github.com.
2. Selecione **Pull Requests** para abrir a lista de PRs.
3. Abra o PR com um título semelhante a **Add missing documentation**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o PR terá a indicação **[WIP]**. Aguarde até que ele conclua o trabalho; isso pode levar alguns minutos.

4. Quando o PR estiver pronto, selecione **Files changed** e revise as alterações.

   ![Guia Files changed](../../../_images/shared-pr-files-changed.png)

5. Examine o código atualizado e os novos comentários TSDoc. Observe também as convenções de TypeScript e os cabeçalhos de comentários das instruções que você revisou no Exercício 2.
6. Volte à guia **Conversation** e role a página.
7. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

8. Acompanhe os fluxos de trabalho na seção de verificações do PR. Confirme se as verificações do projeto para o único aplicativo Astro foram aprovadas. Isso pode levar alguns minutos.

## Solicitar alterações ao GitHub Copilot

Você também pode mencionar o Copilot em comentários do PR ou comentários em linha no código. Ele usará esses comentários para iniciar outra sessão e fazer alterações. Os resultados são não determinísticos; por isso, não há um texto único a fornecer. Você pode pedir, por exemplo, que o Copilot:

- adicione no início de cada arquivo de código um cabeçalho que explique sua finalidade.
- adicione comentários TSDoc aos arquivos TypeScript e Astro.
- crie um README que descreva a estrutura do aplicativo Astro.

1. Adicione um comentário ao PR mencionando **@copilot** e solicite uma alteração na documentação gerada. Use uma das sugestões acima ou indique outra melhoria desejada.
2. Selecione **View Session** para acompanhar a nova sessão do Copilot.
3. Selecione **Back to pull request** para voltar ao PR.

   ![Voltar ao pull request](../../../_images/ex7-back-to-pr.png)

4. Quando o Copilot concluir as alterações, confirme se há um novo commit no PR.
5. Selecione **Files changed** e revise as alterações.

Continue iterando até ficar satisfeito. Depois, marque o PR como pronto para revisão e mescle-o no branch principal.

![Converter o PR em pronto para revisão](../../../_images/ex7-ready-for-review.png)

## Revisar a funcionalidade de jogos relacionados

Agora, revise o PR criado pelo Copilot para exibir jogos relacionados na página de detalhes.

1. Volte ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Abra o PR com um título semelhante a **Show related games on the game details page**.
4. Selecione **Files changed** e revise o código gerado.
5. Depois da revisão, volte à guia **Conversation** e role a página.
6. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

7. Acompanhe as verificações do PR e confirme se foram aprovadas para o único aplicativo Astro.
8. **Opcional:** teste manualmente a funcionalidade no codespace. No terminal, substitua `<branch-name>` pelo branch criado pelo Copilot, por exemplo, `copilot/fix-8`:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

O Copilot criou a funcionalidade de jogos relacionados. Você pode iterar pedindo, por exemplo, que altere a quantidade de jogos exibidos ou adicione cabeçalhos de comentários e comentários TSDoc. Como essa issue foi atribuída antes da atualização das instruções, talvez seja necessário pedir essas mudanças em um comentário na guia **Conversation**. O Copilot iniciará outra sessão.

## Revisar os recursos de acessibilidade

Por fim, revise o PR implementado pelo agente personalizado de acessibilidade. Ele deve incluir tanto o modo de alto contraste solicitado no Exercício 3 quanto o modo claro pedido no Exercício 4.

1. Volte ao repositório no GitHub.com.
2. Selecione a guia **Pull Requests**.
3. Abra o PR com um título semelhante a **Add high contrast mode to website**.

> [!NOTE]
> Se o Copilot ainda estiver trabalhando, o PR terá a indicação **[WIP]**. Aguarde a conclusão, que pode levar alguns minutos.

4. Selecione **Files changed** e revise o código.
5. Examine especialmente:
   - os controles de interface para alternar os modos.
   - o uso do armazenamento local para persistir as preferências.
   - as alterações de CSS ou estilo para os modos de alto contraste e claro.
   - os recursos de acessibilidade, como rótulos de Accessible Rich Internet Applications (ARIA) e navegação por teclado.
   - o código JavaScript/TypeScript que controla a alternância entre modos.
6. Volte à guia **Conversation** e role a página.
7. Se houver fluxos de trabalho aguardando aprovação, selecione **Approve and run workflows**.

   ![Aprovar e executar fluxos de trabalho](../../../_images/shared-approve-workflows.png)

8. Acompanhe as verificações do PR e confirme se foram aprovadas para o único aplicativo Astro.
9. **Opcional:** teste manualmente os recursos de acessibilidade no codespace. No terminal, substitua `<branch-name>` pelo nome do branch criado pelo Copilot:

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

10. Inicie o aplicativo e teste os controles dos modos de alto contraste e claro no navegador. Confirme se funcionam e se as preferências persistem após recarregar a página.

O agente personalizado de acessibilidade orientou o Copilot na implementação de práticas recomendadas. Se encontrar problemas ou melhorias de acessibilidade, mencione **@copilot** em um comentário e solicite alterações, como nos PRs anteriores.

## Exercício opcional: continuar delegando

O agente de nuvem é útil para trabalhar em itens reais do backlog enquanto você se dedica a outras tarefas. Para praticar, crie mais issues no repositório e atribua-as ao Copilot. Algumas ideias:

- criar um formulário de interesse de apoiadores na página de detalhes do jogo.
- implementar paginação na página de listagem de jogos.
- adicionar validação de entrada e tratamento de erros aos helpers de acesso a dados.

## Resumo

Você concluiu o ambiente do agente de nuvem. Ao longo destas lições, você:

- **Inspecionou os arquivos de instruções do projeto** para observar como eles influenciam o trabalho do agente de nuvem.
- **Atribuiu issues ao agente de nuvem do Copilot** e acompanhou a configuração do ambiente, o planejamento e a execução assíncrona.
- **Criou e usou um agente personalizado** para acessibilidade, incluindo controles para os modos de alto contraste e claro.
- **Usou a página de agentes do Copilot como painel central** para monitorar e orientar a sessão de acessibilidade.
- **Revisou e ajustou pull requests do agente de nuvem**, mencionando `@copilot` para solicitar mudanças e aprovando fluxos de trabalho.

## Revisão e próximos passos

Você concluiu o ambiente do agente de nuvem. Os outros ambientes abordam cenários relacionados:

- [Ambiente do VS Code](../../vscode/): explore o modo de agente do Copilot Chat e a integração com MCP no IDE.
- [Ambiente da CLI](../../cli/): entregue duas alterações revisadas no terminal com os modos Plan e Autopilot, skills, um agente de QA, MCP do Playwright, Agent Merge e uma ponte opcional `/delegate` para o agente de nuvem.

No seu repositório, experimente atribuir ao agente de nuvem uma issue de refatoração ou cobertura de testes, criar um agente personalizado para outro domínio ou configurar `copilot-setup-steps.yml` para outra pilha tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Sobre agentes do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de configuração do agente de nuvem][cloud-agent-best-practices]
- [Configurar o firewall do agente de nuvem do Copilot][agent-firewall]

---

| [← Lição anterior: Gerenciar agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
