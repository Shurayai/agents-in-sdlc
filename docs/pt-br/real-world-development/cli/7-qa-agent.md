---
title: "Lição 7 - Criar e usar um agente de garantia de qualidade (QA)"
description: "Crie um agente personalizado de QA que combine requisitos da issue, a skill quality-checks e o MCP do Playwright."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você usou a skill `quality-checks` para executar verificações automatizadas e o Model Context Protocol (MCP) do Playwright para observar a experiência de filtragem no navegador. Agora, reunirá esses recursos em um agente personalizado com um processo de garantia de qualidade (QA) definido.

Nesta lição, você vai:

- explorar como um agente personalizado trabalha com instruções, skills e ferramentas MCP.
- criar e inspecionar um perfil reutilizável de garantia de qualidade.
- selecionar o agente de QA e revisar as descobertas com base na issue de filtragem.

## Cenário

A Tailspin Toys quer uma revisão consistente dos requisitos, da qualidade do código, das verificações automatizadas, da cobertura de testes e do comportamento no navegador antes de abrir um pull request (PR). Um agente personalizado pode coordenar esse processo de QA e gerar um relatório reutilizável.

## O que é um agente personalizado?

Um agente personalizado é uma versão especializada do Copilot, definida em um perfil Markdown. O perfil descreve a finalidade, as instruções e as ferramentas disponíveis para o agente. Neste workshop, você definirá a função de QA em `.github/agents/qa.agent.md` e a selecionará no Copilot CLI.

As personalizações usadas até agora têm funções diferentes. As instruções do repositório descrevem os padrões da equipe. A skill `quality-checks` reúne verificações repetíveis. O MCP do Playwright fornece ferramentas de navegador. O perfil de QA orienta o Copilot sobre como usar esses recursos para avaliar os requisitos e relatar as descobertas. Ele não substitui esses recursos nem exige outra conversa.

## Criar o perfil de QA

Antes de abrir o PR da funcionalidade, peça ao Copilot que crie um perfil de QA reutilizável. O perfil definirá as verificações de QA e os limites que o agente deve respeitar.

1. Volte ao seu codespace e confirme que a conversa de filtragem está no modo Interactive.
2. Peça ao agente padrão que crie o agente personalizado:

   ```plaintext
   Crie um agente personalizado chamado QA em .github/agents/qa.agent.md. Ele deve verificar as funcionalidades com base nas issues e nos requisitos acordados, seguir as instruções do repositório, executar a skill quality-checks, usar o MCP do Playwright para verificar o comportamento e adicionar testes quando a cobertura estiver incompleta.

   Peça que ele classifique cada requisito como aprovado, reprovado ou bloqueado, apresentando evidências. Ele deve pedir autorização antes de alterar o código de implementação e não deve fazer commits nem abrir pull requests.

   Por enquanto, apenas crie o perfil para que eu possa revisá-lo.
   ```

## Inspecionar o perfil

Antes de usar o novo agente, revise o perfil para confirmar se o Copilot capturou o fluxo de QA e os limites pretendidos. Assim, você evita um agente incompleto ou abrangente demais que altere a funcionalidade quando a intenção é apenas verificá-la.

1. Digite `/diff` e abra `.github/agents/qa.agent.md`.
2. Leia o frontmatter. `description` é obrigatório; `name` é opcional, mas sua inclusão dá ao agente um nome claro na interface.
3. Leia as instruções do perfil e confirme se o QA começa pelos requisitos, segue as instruções do repositório, executa a skill `quality-checks` e usa o MCP do Playwright.
4. Confirme se o QA informa evidências, pede autorização antes de alterar o código de implementação e não faz commits nem abre pull requests.
5. Se o perfil gerado não incluir alguma dessas responsabilidades ou algum desses limites, peça ao agente padrão que o revise antes de continuar.

## Executar o QA com base na issue

O Copilot CLI carrega os agentes do projeto quando uma conversa é iniciada. Depois de criar o perfil, retome a mesma conversa de filtragem e selecione o QA para que ele possa usar a issue e as decisões de planejamento já presentes no contexto.

1. Ative o agente com este prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como você acabou de criar o agente, talvez ele não apareça na lista de agentes disponíveis. Mesmo assim, o comando acima o ativará.

2. Use este prompt para pedir ao agente de QA que revise a funcionalidade:

   ```plaintext
   Revise a funcionalidade de filtragem com base na issue e nas decisões do nosso plano. Ela está pronta para um PR?
   ```

3. Aguarde enquanto o agente de QA trabalha.
4. Quando terminar, leia o relatório.

## Resumo e próximos passos

Você adicionou uma função especialista reutilizável ao fluxo de trabalho e revisou o trabalho dela. Nesta lição, você:

- explorou como um agente personalizado trabalha com instruções, skills e ferramentas MCP.
- criou e inspecionou um perfil reutilizável de garantia de qualidade.
- selecionou o agente de QA e revisou as descobertas com base na issue de filtragem.

Agora, você tem a implementação, a atualização da skill, o perfil de QA, os testes e o relatório de verificação prontos para revisão. Em seguida, você [reunirá esses itens em um PR de funcionalidade e usará o Agent Merge][next-lesson].

## Recursos

- [Criar agentes personalizados para o Copilot CLI][create-agents]
- [Configuração de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
