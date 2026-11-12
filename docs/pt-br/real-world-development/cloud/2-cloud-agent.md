---
title: "Exercício 2 - Agente de nuvem do GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lição anterior: Instruções personalizadas][previous-lesson] |
|:--|

É comum que organizações tenham dificuldades com dívida técnica: problemas de segurança não resolvidos, código legado que precisa de atualização ou solicitações de funcionalidades que permanecem no backlog por falta de tempo. O agente de nuvem do GitHub Copilot pode atualizar código e adicionar funcionalidades de forma autônoma. Ao concluir o trabalho, ele cria um pull request (PR) de rascunho para revisão por uma pessoa desenvolvedora. Assim, é possível delegar tarefas demoradas e se concentrar em outras prioridades.

Neste exercício, você explorará como:

- personalizar o ambiente de geração de código.
- garantir que as operações sejam realizadas com segurança.
- criar issues com escopo claro.
- atribuir issues ao Copilot.

## Cenários

A Tailspin Toys quer resolver parte da dívida técnica. A documentação deixada pelos prestadores que criaram a primeira versão do site está completamente ausente. Como primeiro passo, a equipe quer adicionar comentários TSDoc a todas as funções exportadas do aplicativo.

A equipe de design também quer facilitar a descoberta de jogos. Cada página de detalhes deve mostrar jogos relacionados — outros títulos da mesma categoria — para que as pessoas possam continuar explorando. Por enquanto, a equipe precisa apenas de uma implementação que permita testar a experiência de usuário (UX). Essa tarefa está bloqueada, mas há issues prioritárias no momento.

Esses são exemplos de trabalho que pode ser adiado. O agente de nuvem do Copilot pode trabalhar neles de forma assíncrona enquanto você se dedica a outras tarefas e, depois, revisa as alterações.

## Conhecer o agente de nuvem do GitHub Copilot

O [agente de nuvem do GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) pode executar tarefas em segundo plano de forma semelhante a uma pessoa desenvolvedora. Por exemplo, você pode [atribuir uma issue do GitHub ao Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Depois da atribuição, o Copilot cria um pull request de rascunho para acompanhar o progresso, configura um ambiente e começa a trabalhar. Você pode acompanhar a sessão enquanto o trabalho acontece ou depois de concluído. Quando a solução estiver pronta para revisão, o Copilot mencionará você no pull request.

## A importância de instruções com escopo claro

O GitHub Copilot não elimina a necessidade de pensar. Mesmo tarefas aparentemente simples podem ter complexidades, portanto defina o escopo cuidadosamente ao [atribuir tarefas ao agente de nuvem][cloud-agent-best-practices]. Trate-o como um parceiro de programação com inteligência artificial (IA): trabalhe em etapas, aprenda, experimente e adapte o processo. A inclusão de IA generativa não muda os fundamentos do desenvolvimento de software.

## Instruções personalizadas neste repositório

As lições anteriores apresentaram instruções personalizadas e como elas orientam o Copilot. Antes de atribuir trabalho ao agente de nuvem, examine os arquivos de instruções incluídos no repositório, sem alterá-los.

1. Abra `.github/copilot-instructions.md` na interface Web do GitHub ou em um codespace. Revise **Code standards**, principalmente as convenções de TypeScript e os comentários TSDoc.
2. Abra `.github/instructions/unit-tests.instructions.md` e observe o frontmatter `applyTo`, que associa as instruções aos arquivos `**/*.test.ts`.

Na próxima seção, atribua ao agente a issue `Code lacks documentation` e observe no pull request os comentários TSDoc, as convenções de TypeScript e os cabeçalhos de comentários definidos por esses arquivos.

## Configurar o ambiente de desenvolvimento do agente de nuvem

O agente de nuvem usa [GitHub Actions][github-actions] para configurar o ambiente de trabalho. Você pode criar um [fluxo de configuração especial][setup-workflow] em `.github/workflows/copilot-setup-steps.yml`, executado antes do início do trabalho, para instalar ferramentas e dependências necessárias.

Esse fluxo já está configurado no laboratório. Ele disponibiliza Node.js, dependências do projeto, navegadores para testes de ponta a ponta e o banco de dados SQLite migrado e preenchido da aplicação Astro:

```yaml
name: "Copilot Setup Steps"

# Permite testar as etapas de configuração na guia "Actions" do repositório
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Defina as permissões mínimas necessárias para *suas etapas*. O Copilot receberá um token próprio para as operações dele.
    permissions:
      # Para clonar o repositório nas etapas de configuração, por exemplo, para instalar dependências, será necessária a permissão `contents: read`. Se as etapas não clonarem o repositório, o Copilot fará isso automaticamente depois que elas forem concluídas.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuração do frontend/aplicativo - Node.js (todo o aplicativo agora usa Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migre e preencha o banco de dados SQLite local para que compilações e testes tenham dados.
      - name: Set up the database
        run: npm run db:setup
```

Esse arquivo se parece com outros fluxos de trabalho do GitHub, mas tem alguns pontos importantes:

- Ele contém um único trabalho, `copilot-setup-steps`, executado no GitHub Actions antes de o Copilot começar a trabalhar no pull request.
- O gatilho `workflow_dispatch` permite executar o fluxo manualmente na guia **Actions** do repositório para verificar se ele funciona.

## Adicionar documentação

A documentação costuma ficar desatualizada ou não existir, o que dificulta a manutenção do código e a integração de novas pessoas na equipe. O Copilot pode criar documentação em segundo plano, então essa é uma boa tarefa para atribuir ao agente de nuvem. Você revisará o trabalho em um exercício futuro.

1. Em uma nova guia do navegador, acesse seu repositório no github.com.
2. Selecione a guia **Issues** e, em seguida, **New issue**.
3. Selecione **Blank issue**.
4. No campo **Title**, digite `Code lacks documentation`.
5. No campo **Description**, digite:

   ```plaintext
   Nossa organização exige que as funções e os métodos tenham comentários TSDoc quando eles forem úteis. Infelizmente, atualizações recentes não seguiram esse padrão. Precisamos atualizar o código existente para incluir comentários quando eles ajudarem a esclarecer o comportamento.
   ```

6. Selecione **Create** para criar a issue.
7. À direita, selecione **Assign to Copilot** e, na caixa de diálogo, selecione **Assign**.

   ![Atribuição do Copilot a uma issue](../../../_images/shared-assign-copilot.png)

8. Selecione a guia **Pull Requests** e abra o novo PR, provavelmente intitulado algo como `[WIP]: Code lacks documentation`. Se ele ainda não aparecer, aguarde um ou dois minutos e atualize a página.
9. Aguarde a criação da lista de tarefas pelo Copilot. Isso pode levar alguns minutos enquanto ele configura o ambiente, analisa o projeto e define uma abordagem.
10. Revise a lista de tarefas e role a linha do tempo do PR para acompanhar o início do trabalho.
11. Selecione **View session** para acompanhar a sessão ao vivo e observar a exploração do código, o planejamento e a implementação.

   ![Detalhes da atribuição do Copilot](../../../_images/ex4-assign-copilot-details.png)

   ![Visualização da sessão do Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Talvez seja necessário atualizar a janela para ver o indicador de estado atualizado.

O trabalho pode levar alguns minutos. Enquanto o agente trabalha, você pode atribuir outra tarefa e continuar com outras atividades.

## Adicionar uma seção de jogos relacionados

A execução assíncrona permite dividir o trabalho: enquanto o agente cuida de uma tarefa, você pode se dedicar a outras. Atribua ao agente a implementação de uma seção de jogos relacionados na página de detalhes.

1. Volte ao repositório no github.com e selecione **Issues** > **New issue** > **Blank issue**.
2. No campo **Title**, digite `Show related games on the game details page`.
3. No campo **Description**, digite:

   ```markdown
   Queremos ajudar as pessoas a descobrir mais jogos exibindo jogos relacionados na página de detalhes de cada jogo. A equipe de design quer explorar a experiência e fazer testes de aceitação. Requisitos:

   - Adicione um helper de acesso a dados em `src/lib/` que retorne outros jogos da mesma categoria de um jogo, sem incluir o próprio jogo.
   - Exiba uma seção "Related games" na página de detalhes do jogo usando o helper.
   - Trate o caso em que um jogo não tenha jogos relacionados.
   - Crie testes unitários para o novo helper.
   - Antes de criar o PR, confirme que todos os testes foram aprovados.
   ```

4. Selecione **Create** e, na lateral direita, selecione **Assign to Copilot**.
5. Na caixa de diálogo de atribuição, selecione **Assign**.

   ![Atribuição do Copilot a uma issue](../../../_images/shared-assign-copilot.png)

O Copilot indicará que está trabalhando na issue. Você não precisa acompanhá-lo continuamente; revise o trabalho quando estiver concluído.

![O emoji de olhos indica que o Copilot está trabalhando na issue](../../../_images/ex4-issue-eyes-emoji.png)

## Resumo e próximos passos

Você explorou o [agente de nuvem do GitHub Copilot][copilot-agents], que permite atribuir issues para execução assíncrona. Ele pode ajudar a resolver dívida técnica, criar funcionalidades ou migrar código entre frameworks.

Nesta lição, você:

- personalizou o ambiente de geração de código.
- explorou como manter as operações seguras.
- aprendeu sobre o escopo claro das issues.
- atribuiu issues ao Copilot.

Enquanto o agente trabalha, você pode criar e usar agentes personalizados. O [agente de nuvem também pode usar servidores MCP][cloud-agent-mcp] e as instruções personalizadas exploradas nas lições anteriores.

## Recursos

- [Sobre o agente de nuvem do Copilot][copilot-agents]
- [Atribuir issues do GitHub ao Copilot][assign-issue]
- [Práticas recomendadas para o fluxo de configuração do agente de nuvem][cloud-agent-best-practices]

| [Próxima lição: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
