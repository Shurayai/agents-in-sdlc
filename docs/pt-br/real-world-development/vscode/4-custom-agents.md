---
title: "Exercício 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## O que são agentes personalizados?

Os [agentes personalizados][custom-agents-concept] do GitHub Copilot permitem criar assistentes de inteligência artificial (IA) especializados em tarefas ou domínios do fluxo de desenvolvimento. Defina-os em arquivos Markdown na pasta `.github/agents` do repositório, com instruções específicas, práticas recomendadas, padrões de codificação e conhecimento de domínio. As equipes podem registrar sua experiência em agentes reutilizáveis, como agentes de acessibilidade, segurança ou testes.

Os agentes podem ser definidos em `.github/agents` no projeto ou globalmente em `~/.copilot/agents`. Cada arquivo tem frontmatter YAML com pelo menos `name` e `description`, seguido de um prompt Markdown que define o comportamento, a experiência e as instruções do agente.

### Agentes personalizados e skills de agente

Há alguma sobreposição entre agentes personalizados e [skills de agente][agent-skills-concept]. Ambos são definidos principalmente em arquivos Markdown e orientam o trabalho de IA. Uma distinção útil é: um **agente personalizado** é quem executa o trabalho; as **skills** são as ferramentas.

Os agentes personalizados têm sua própria janela de contexto e podem orquestrar skills e outros agentes. Neste laboratório, o agente de acessibilidade revisará e atualizará o site conforme as diretrizes de acessibilidade, podendo chamar skills para fluxos de pull request ou execução e gerenciamento de testes.

> [!NOTE]
> Não há uma única maneira certa de criar um agente. Teste e itere para encontrar o que funciona para seus ambientes e cenários.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Cenário

A Tailspin Toys quer tornar sua plataforma de financiamento coletivo acessível a todas as pessoas, independentemente de suas capacidades ou preferências visuais. Comentários de usuários indicam que algumas pessoas têm dificuldade para ler o tema escuro por causa do contraste insuficiente. A equipe de design solicitou um modo de alto contraste que possa ser ativado e desativado.

Neste exercício, você vai:

- revisar um agente personalizado de acessibilidade existente.
- usar o agente no Copilot Chat para implementar o modo de alto contraste.

## Revisar o agente personalizado de acessibilidade

O agente de acessibilidade já foi criado. Revise as instruções para entender como elas orientarão o Copilot.

1. Volte ao codespace e, no terminal, crie um branch novo a partir de `main` para manter o PR de filtragem do Exercício 3 separado:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. Abra `.github/agents/accessibility.md` e observe os campos `name` e `description` no frontmatter YAML.

> [!CAUTION]
> Os campos `name` e `description` são obrigatórios no frontmatter de agentes personalizados.

3. Leia as seções sobre responsabilidades para gerar código acessível, práticas recomendadas, exemplos de HTML, CSS e JavaScript e erros comuns.

## Usar o agente personalizado no Copilot Chat

O VS Code exibe os agentes personalizados definidos em `.github/agents` na lista de agentes na parte inferior da visualização Copilot Chat. Selecione um agente para aplicar suas instruções e ferramentas à conversa.

> [!TIP]
> **Abrir o Copilot Chat**
>
> Volte ao codespace, abra o painel do Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; cada etapa especificará as opções necessárias.

1. Na lista de agentes, selecione **Agent**, se ainda não estiver selecionado.

   ![Captura de tela do seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

2. Abra a lista de agentes na parte inferior da visualização de chat. Por padrão, o agente ativo é **default**.
3. Selecione **Accessibility agent**.
4. Envie este prompt ao agente:

   ```plaintext
   Adicione ao site um modo de alto contraste com um controle que a pessoa usuária possa ativar. A configuração deve persistir entre recarregamentos da página usando o armazenamento local do navegador.
   ```

5. O Copilot Chat explorará a base de código, proporá alterações e editará os arquivos do projeto. Cada edição aparecerá no chat com o caminho do arquivo e uma diferença para revisão.
6. Observe o indicador **Files changed**, que é atualizado à medida que o agente altera arquivos.

> [!NOTE]
> Esse processo pode levar alguns minutos. O Copilot alterará arquivos do repositório, como componentes Astro, CSS e testes relacionados.

Na próxima lição, você acompanhará e orientará esse trabalho em andamento.

## Resumo e próximos passos

Você explorou [agentes personalizados][custom-agents], assistentes de IA especializados em tarefas e domínios específicos. Eles permitem registrar a experiência e os padrões da equipe em agentes reutilizáveis que orientam o trabalho do Copilot.

Nesta lição, você:

- revisou como agentes personalizados são definidos.
- usou um agente personalizado no modo de agente do Copilot Chat.

Em seguida, você [acompanhará e orientará o trabalho do agente][next-lesson], revisando as alterações e adicionando um controle do modo claro à mesma sessão.

## Recursos

- [Sobre agentes personalizados][custom-agents]
- [Criar agentes personalizados no IDE][creating-custom-agents-ide]
- [Agentes personalizados no VS Code][custom-agents-vscode]
- [Configuração de agentes personalizados][custom-agents-config]
- [Agentes personalizados no awesome-copilot][awesome-copilot-agents]

---

| [← Lição anterior: Testar a funcionalidade com o servidor MCP do Playwright][previous-lesson] | [Próxima lição: Monitorar e gerenciar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
