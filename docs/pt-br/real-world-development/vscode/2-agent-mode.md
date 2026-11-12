---
title: "Exercício 2 - Adicionar funcionalidades com o modo de agente do Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Até mesmo uma pequena atualização de um aplicativo pode exigir mudanças em vários arquivos e a execução de testes. Em geral, o fluxo envolve localizar os arquivos, fazer as alterações, executar testes, depurar e descobrir o que ficou faltando. O modo de agente do Copilot pode explorar a estrutura do projeto, coordenar alterações em arquivos, executar tarefas como testes e corrigir problemas encontrados.

> [!NOTE]
> Apesar dos nomes semelhantes, o modo de agente e o agente de nuvem oferecem experiências diferentes. O modo de agente trabalha no ambiente de desenvolvimento integrado (IDE), com ciclos rápidos de feedback e interação. O agente de nuvem trabalha de forma assíncrona, como uma pessoa da equipe, e interage com você por meio de issues e pull requests.

Neste exercício, você aprenderá como:

- o modo de agente do Copilot explora o projeto, identifica arquivos relevantes e coordena alterações.
- o modo de agente implementa funcionalidades na interface e na camada de dados.
- revisar alterações e testes gerados pelo Copilot antes de mesclá-los à base de código.

## Cenário

À medida que a lista de jogos cresce, você quer permitir a filtragem por categoria e editora. No exercício anterior, você adicionou um helper de editoras. Agora, concluirá o trabalho restante na camada de dados, na interface e nos testes usando o modo de agente do Copilot.

## Executar o site Tailspin Toys

Antes de alterar o código, explore o site para conhecer o comportamento atual. O site de financiamento coletivo para jogos de tabuleiro com tema de desenvolvimento é um único aplicativo Astro, que gera HyperText Markup Language (HTML) estático durante a compilação. As páginas consultam diretamente um banco de dados SQLite local pelo Drizzle, um mapeador objeto-relacional (ORM). Não há uma interface de programação de aplicações (API) de backend separada nem um framework de interface no cliente. Os helpers de acesso a dados ficam em `src/lib/`; a interatividade usa um elemento `<script>` do Astro com APIs padrão do Document Object Model (DOM).

### Iniciar o site

O comando `npm run dev` inicia o servidor de desenvolvimento Astro.

1. Volte ao codespace. Você deve estar no branch `main` depois do exercício anterior.
2. Abra um terminal com <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Atualize `main` e crie um branch para a filtragem:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicie o site:

   ```bash
   npm run dev
   ```

   Quando o servidor Astro estiver pronto, você verá uma mensagem semelhante a:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

5. Se aparecer uma caixa de diálogo perguntando se deseja abrir `http://localhost:4321`, feche-a selecionando **x**.
6. Abra o site mantendo pressionada a tecla <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando `http://localhost:4321` no terminal.

> [!NOTE]
> No Codespaces, o link localhost do terminal redireciona para `https://<your-codespace-name>-4321.app.github.dev/`, um túnel privado para o servidor do codespace.

### Explorar o site

O site lista jogos e exibe seus detalhes.

- **Home Page**: mostra jogos com títulos, imagens e descrições.
- **Game Details Page**: quando você seleciona um jogo, abre a página de detalhes com informações como título, descrição, editora e categoria.

## Explorar o backlog com o Copilot

> [!TIP]
> **Abrir o Copilot Chat**
>
> Volte ao codespace, abra o painel do Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; cada etapa especificará as opções necessárias.

O backlog de issues foi criado quando você configurou o projeto a partir do modelo. Peça ao GitHub Copilot que o apresente.

1. Na lista de agentes da visualização Chat, selecione **Agent** para que ele planeje e implemente alterações em arquivos, execute comandos e use ferramentas.

   ![Captura de tela do seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

2. Na lista de modelos disponíveis, selecione **Claude Sonnet 4.5**.

> [!CAUTION]
> A inclusão desse modelo não representa uma preferência dos autores. Ele foi usado durante a criação do workshop para que as sugestões fossem relativamente consistentes. Como os modelos de linguagem são probabilísticos, os resultados podem diferir dos exemplos; isso é normal.

> [!NOTE]
> O Copilot pode usar um comando MCP diferente, mas ainda deverá concluir a tarefa.

3. Envie este prompt:

   ```plaintext
   Mostre o backlog de itens do meu repositório do GitHub. Ajude-me a priorizá-los com base no que será mais útil para as pessoas usuárias.
   ```

4. Selecione **Continue** para executar o comando que lista as issues.
5. Revise a lista gerada.

## Revisar os arquivos de instruções

Antes de pedir ao agente que gere código, revise o arquivo de instruções da interface do usuário, que fornece contexto sobre como adicionar funcionalidades ao site.

1. No codespace, abra `.github/instructions/ui.instructions.md`.
2. Observe as orientações sobre arquitetura, componentes, capacidade de teste e acessibilidade, além dos links para instruções de Astro, Tailwind CSS e Drizzle.

> [!TIP]
> Os arquivos de instruções podem referenciar outros arquivos de instruções e arquivos do projeto. Os caminhos são relativos ao arquivo de instruções, o que permite reutilizar conteúdo e fornecer exemplos.

## Implementar a filtragem

Para concluir a filtragem, são necessárias alterações na lógica da camada de dados em `src/lib/`, nos testes e na página de listagem de jogos. O modo de agente do Copilot pode realizar essas tarefas.

1. Continue a conversa atual ou selecione **New Chat** para iniciar outra.
2. Selecione **Add Context**, **Instructions** e **ui** como arquivo de instruções.

   ![Captura de tela da seleção do arquivo de instruções da interface](../../../_images/ex3-select-instructions-file.png)

3. Confirme que **Agent** continua selecionado na lista de agentes.

   ![Captura de tela do seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirme que **Claude Sonnet 4.5** continua selecionado.
5. Peça ao Copilot que implemente a funcionalidade com base na issue:

   ```plaintext
   Atualize o site para incluir a filtragem por editora e categoria conforme os requisitos da issue relacionada no backlog do GitHub. Um helper de editoras já existe por causa do exercício anterior; preserve e refine esse trabalho conforme necessário enquanto conclui as alterações restantes na camada de dados, na interface e nos testes. Confirme que todos os testes foram aprovados. O servidor já está em execução, então não precisa iniciá-lo.
   ```

6. Acompanhe o Copilot enquanto ele explora o projeto, localiza os arquivos relevantes e altera os helpers de dados, a interface e os testes.

   ![Captura de tela do Copilot explorando os arquivos do projeto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> A tarefa pode levar alguns minutos. Durante o trabalho, os botões **Keep** e **Undo** podem aparecer no editor. Aguarde a conclusão antes de aceitar ou desfazer as alterações.

7. Quando solicitado pelo Copilot, selecione **Continue** para executar os testes.
8. Alguns testes podem falhar durante o processo; o Copilot pode iterar entre geração de código e testes até não detectar erros.
9. Inspecione o código gerado para identificar possíveis problemas.

   ![Captura de tela de uma sessão completa do Copilot no modo de agente](../../../_images/ex3-agent-mode-proposed-changes.png)

> [!CAUTION]
> Revise sempre o código gerado pelo Copilot ou por outras ferramentas de IA.

10. Volte ao navegador em que o site está em execução e explore a nova funcionalidade.
11. Depois de confirmar o funcionamento e revisar o código, selecione **Keep** na janela do Copilot Chat.

## Resumo e próximos passos

Você explorou como usar o modo de agente do GitHub Copilot para adicionar funcionalidades ao site Tailspin Toys. Nesta lição, você aprendeu como:

- implementar funcionalidades na interface e na camada de dados com o modo de agente.
- explorar o projeto, identificar arquivos relevantes e coordenar alterações.
- revisar alterações e testes gerados antes da mesclagem.

Em seguida, você [testará a funcionalidade com o servidor MCP do Playwright][next-lesson] e abrirá um pull request.

### Exercício extra: implementar paginação

À medida que a lista de jogos cresce, será necessário adicionar paginação. Use as habilidades deste exercício e peça ao Copilot que atualize o site. Considere se o tamanho da página será fixo ou se poderá ser escolhido pela pessoa usuária, forneça o contexto necessário e itere sobre as sugestões.

## Recursos

- [Copilot: modos Ask, Edit e Agent — o que fazem e quando usar][choose-mode]
- [Modo de agente no VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
