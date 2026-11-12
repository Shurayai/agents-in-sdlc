---
title: "Lição 6 - Validar funcionalidades com o Model Context Protocol (MCP) do Playwright"
description: "Inspecione ou configure o servidor MCP do Playwright no Copilot CLI e use-o para explorar a filtragem em um navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como já destacamos, desenvolver software envolve mais do que escrever código. Também é preciso trabalhar com dados, serviços externos e automações adicionais disponíveis para o Copilot. É aí que entram os servidores do Model Context Protocol (MCP): eles ampliam as ferramentas e os serviços disponíveis no Copilot CLI.

Nesta lição, você vai:

- entender o Model Context Protocol (MCP) e como o Copilot CLI o usa.
- adicionar o servidor MCP do Playwright, se ele ainda não estiver disponível.
- pedir ao agente que controle um navegador e explore a filtragem.

## Cenário

Testes unitários e de ponta a ponta são importantes, mas validar mudanças na interface do usuário (UI) exige interagir com ela. Você permitirá que o Copilot use o site como uma pessoa usuária para automatizar a validação e aumentar a confiança de que as mudanças funcionam como esperado.

## O que é Model Context Protocol (MCP)?

O [Model Context Protocol (MCP)][mcp-blog-post] permite que agentes de inteligência artificial (IA) se comuniquem com ferramentas e serviços externos em tempo real. Assim, eles podem acessar informações atualizadas e executar ações em seu nome.

Essas ferramentas e esses recursos são acessados por meio de um servidor MCP, que atua como ponte entre o agente de IA e as ferramentas e os serviços externos. Cada servidor MCP oferece um conjunto diferente de ferramentas e recursos.

Alguns servidores MCP conhecidos:

- **[Servidor MCP do GitHub][github-mcp]**: oferece acesso a APIs para gerenciar repositórios, issues e pull requests do GitHub.
- **[Servidor MCP do Playwright][playwright-mcp-server]**: oferece recursos de automação de navegador com Playwright.

Há muitos outros servidores MCP. O GitHub mantém um [registro MCP][mcp-registry] para facilitar a descoberta de servidores e as contribuições ao ecossistema.

> [!CAUTION]
> Trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor, revise o código-fonte, verifique o publicador e considere as implicações de segurança.

## Adicionar o servidor MCP do Playwright

Se o servidor MCP do Playwright ainda não estiver disponível, adicione-o para que o Copilot possa interagir com o site como uma pessoa usuária.

> [!NOTE]
> Se o MCP do Playwright já estiver configurado no Copilot CLI, ignore estas etapas e continue na próxima seção.

1. Volte ao codespace.
2. No Copilot CLI, digite este comando para abrir a caixa de diálogo de adição de servidor MCP:

   ```plaintext
   /mcp add
   ```

3. Digite `playwright` como nome e pressione <kbd>Tab</kbd>.
4. Confirme o tipo de servidor **STDIO** pressionando <kbd>Enter</kbd> e, em seguida, pressione <kbd>Tab</kbd>.
5. Cole este comando na caixa de diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pressione <kbd>Control</kbd>+<kbd>S</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para salvar o novo servidor MCP.
7. Pressione <kbd>Esc</kbd> para sair da caixa de diálogo do MCP.

## Pedir ao Copilot que explore a funcionalidade com o Playwright

Você já confirmou manualmente que a funcionalidade funciona. Agora, use o servidor MCP do Playwright disponível no Copilot para fazer o mesmo.

1. Envie este prompt para pedir ao Copilot que use o servidor MCP do Playwright para validar a funcionalidade:

   ```plaintext
   Inicie o aplicativo e use o MCP do Playwright para verificar a filtragem com base na issue e no nosso plano. Informe o que funciona e o que não funciona, sem fazer alterações. Encerre o servidor que iniciou quando terminar.
   ```

> [!NOTE]
> Não é obrigatório indicar o servidor MCP ao Copilot; normalmente, ele o identifica sozinho. Mas especificá-lo pode ajudar a orientar o trabalho e tornar os resultados mais consistentes.

2. Observe as etapas executadas pelo Copilot no navegador para confirmar se a funcionalidade funciona.
3. Leia o relatório e confira se tudo se comporta como esperado.

O Copilot iniciará o servidor, usará o Playwright para interagir com o site, encerrará o servidor e apresentará um relatório.

## Resumo e próximos passos

Você usou o servidor MCP do Playwright para explorar sua funcionalidade em um navegador real por meio do Copilot CLI. Nesta lição, você:

- aprendeu o que é o Model Context Protocol (MCP) e como o Copilot CLI o usa.
- adicionou o servidor MCP do Playwright, caso ele ainda não estivesse disponível.
- pediu ao agente que controlasse um navegador e explorasse a filtragem.

Em seguida, você [criará um agente personalizado de QA][next-lesson] que reunirá a skill e as ferramentas de navegador em uma função especialista.

## Recursos

- [O que é MCP e por que todo mundo está falando sobre isso?][mcp-blog-post]
- [Servidor MCP do Microsoft Playwright][playwright-mcp-server]
- [Adicionar servidores MCP ao Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
