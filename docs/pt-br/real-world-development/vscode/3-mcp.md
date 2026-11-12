---
title: "Exercício 3 - Testar a funcionalidade com o Model Context Protocol (MCP) do Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Modo de agente][previous-lesson] · [Próxima lição: Agentes personalizados →][next-lesson]

Você acabou de criar a filtragem com o modo de agente. Antes de abrir um pull request, confirme que ela funciona no navegador. Em vez de testar o aplicativo manualmente, conecte o **servidor do Model Context Protocol (MCP) do Playwright** e peça ao Copilot que controle um navegador real. Depois, publique o branch e abra o PR.

Neste exercício, você vai:

- aprender o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionar o servidor MCP do Playwright ao workspace.
- pedir ao Copilot que o use para testar manualmente a filtragem em um navegador.
- publicar o branch e abrir um pull request para o trabalho de filtragem.

## O que é Model Context Protocol (MCP)?

O modo de agente fica mais poderoso quando pode acessar ferramentas externas. O Model Context Protocol (MCP) é um padrão para a comunicação entre o agente do Copilot e ferramentas e serviços externos.

![Diagrama do funcionamento interno do modo de agente e da interação com contexto, modelo de linguagem de grande porte (LLM) e ferramentas, incluindo ferramentas fornecidas por servidores MCP e extensões do VS Code](../../../_images/ex1-mcp-diagram.png)

O [Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite que agentes de IA se comuniquem com ferramentas e serviços externos em tempo real. Eles podem acessar informações atualizadas por meio de recursos e executar ações em seu nome por meio de ferramentas.

Um servidor MCP faz a ponte entre o agente e essas ferramentas e serviços, como APIs existentes ou ferramentas locais. Cada servidor oferece um conjunto diferente de ferramentas e recursos.

- O **[servidor MCP do GitHub](https://github.com/github/github-mcp-server)** oferece acesso a APIs para gerenciar repositórios, issues e pull requests do GitHub.
- O **[servidor MCP do Playwright](https://github.com/microsoft/playwright-mcp)** oferece automação de navegador, como navegar em páginas, preencher formulários e selecionar botões.

Há muitos outros servidores MCP. O GitHub mantém um [registro MCP](https://github.com/mcp) para facilitar a descoberta de servidores e as contribuições ao ecossistema.

> [!CAUTION]
> Trate os servidores MCP como qualquer outra dependência do projeto. Antes de usar um servidor, revise o código-fonte, verifique o publicador e considere as implicações de segurança. Use apenas servidores confiáveis e tenha cuidado ao conceder acesso a recursos ou operações confidenciais.

## Revisar a configuração do MCP

O arquivo `.vscode/mcp.json` configura os servidores MCP disponíveis neste workspace do VS Code.

1. Abra `.vscode/mcp.json` no codespace.
2. Observe que já há um servidor `github` configurado:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

Essa entrada vem do modelo do projeto e permitiu que o Copilot lesse o backlog de issues no exercício anterior. Ela usa o [servidor MCP remoto do GitHub][remote-github-mcp-server], ao qual o VS Code se conecta por HTTP. Não é necessário instalá-lo localmente; autentique-se no GitHub na primeira vez que o Copilot usar uma ferramenta.

## Adicionar o servidor MCP do Playwright

Adicione um segundo servidor. O [servidor MCP do Playwright][playwright-mcp-server] fornece ao Copilot um navegador que ele pode controlar para testar a funcionalidade.

1. Em `.vscode/mcp.json`, adicione uma entrada `playwright` ao lado de `github`:

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. Salve o arquivo.

Ao contrário do servidor remoto `github`, `playwright` é local: o VS Code o inicia na máquina executando `npx @playwright/mcp@latest`. A opção `--headless` executa o navegador sem uma janela visível, necessária no codespace, que não tem uma área de trabalho gráfica.

> [!NOTE]
> O projeto Tailspin Toys já usa o Playwright para testes de ponta a ponta, então o navegador necessário geralmente já está instalado. Se o Copilot informar que não há navegador, peça que execute `npx playwright install chromium` e tente novamente.

## Iniciar e confiar no servidor

O VS Code inicia servidores MCP **sob demanda**: quando o Copilot precisa das ferramentas de um servidor pela primeira vez, o VS Code o inicia e pede que você confirme se confia nele.

1. Em `.vscode/mcp.json`, selecione a ação **Start** que aparece acima da entrada `playwright` para iniciar o servidor e confirmar a configuração.
2. Se o VS Code perguntar se você confia no servidor, revise a configuração e confirme para iniciá-lo.

Iniciar o servidor manualmente é opcional. Se você não fizer isso, o VS Code o iniciará e pedirá confirmação quando o Copilot precisar das ferramentas na próxima etapa.

## Testar a filtragem

Com o servidor conectado e o aplicativo em execução, peça ao Copilot que teste a filtragem:

```text
Usando o servidor MCP do Playwright, abra um navegador para o aplicativo em execução em http://localhost:4321 e verifique a nova filtragem de jogos:

1. Acesse a página de jogos e informe quantos jogos estão listados.
2. Aplique um filtro de categoria e confirme se a lista mostra somente os jogos dessa categoria.
3. Remova o filtro e aplique um filtro de editora. Confirme se a lista mostra somente os jogos dessa editora.
4. Combine um filtro de categoria e um de editora e confirme se os resultados respeitam ambos.

Informe o que observou em cada etapa e destaque qualquer comportamento inesperado.
```

O Copilot abrirá um navegador pelo servidor MCP do Playwright, seguirá as etapas e apresentará um relatório. Compare-o com os critérios de aceitação da issue. Se houver problemas, faça perguntas ou peça ao Copilot que corrija o código antes de abrir o pull request.

O servidor MCP do Playwright usa a árvore de acessibilidade da página, não capturas de tela. Assim, o agente examina elementos estruturados e rotulados, como botões, links e itens de lista, de forma semelhante às tecnologias assistivas. Uma verificação funcional também pode servir como uma análise básica de acessibilidade.

> [!NOTE]
> Para este teste, o aplicativo precisa estar em execução em `http://localhost:4321`. Se o servidor de desenvolvimento tiver sido encerrado, inicie-o novamente. Na primeira utilização, o Playwright pode precisar baixar um navegador; se o Copilot informar que falta um navegador, peça que execute `npx playwright install chromium` e tente novamente.

## Publicar o branch e criar um pull request

Depois de confirmar que a funcionalidade funciona, publique o branch `filtering-vscode`.

1. Abra o painel **Source Control** no codespace e revise as alterações feitas pelo Copilot.
2. Selecione o ícone **+** para preparar as alterações.
3. Use o botão **Sparkle** para gerar uma mensagem de commit.

   ![Captura de tela do painel Source Control com as alterações feitas](../../../_images/ex3-source-control-changes.png)

4. Selecione **Publish** para enviar o branch ao repositório.

## Criar o pull request

O Copilot pode encontrar a issue relevante e criar um PR associado a ela.

1. No painel Copilot Chat, selecione **New Chat** para iniciar uma sessão.
2. Confirme que **Agent** está selecionado na lista de agentes para que o Copilot possa usar as ferramentas do GitHub.
3. Peça ao Copilot que crie o PR:

   ```plaintext
   Encontre no repositório a issue relacionada à filtragem por categoria e editora. Crie um pull request para o branch atual e associe-o à issue correta.
   ```

4. Quando necessário, selecione **Continue** para permitir que o Copilot obtenha informações e execute ações. Na primeira utilização de uma ferramenta do GitHub, talvez seja necessário autenticar-se.
5. Observe o Copilot pesquisar as issues, encontrar a correta e criar o PR.
6. Abra o link gerado pelo Copilot para revisar o PR, mas **não o mescle ainda**.

## Resumo e próximos passos

Neste exercício, você:

- aprendeu o que é o Model Context Protocol (MCP) e como os servidores MCP ampliam as ferramentas do Copilot.
- adicionou o servidor MCP do Playwright ao workspace.
- usou o servidor para testar a filtragem em um navegador antes de publicar a alteração.
- publicou o branch e abriu um pull request para o trabalho de filtragem.

Você usou um servidor MCP para testar uma funcionalidade, mas o MCP também pode ampliar o Copilot de outras maneiras. Em seguida, [crie um agente personalizado][next-lesson] para agilizar tarefas específicas, como revisões de acessibilidade.

## Recursos

- [O que é MCP e por que todo mundo está falando sobre isso?][mcp-blog-post]
- [Servidor MCP do Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP do GitHub][github-mcp-server]
- [Registro MCP do GitHub][mcp-registry]
- [Servidores MCP no VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
