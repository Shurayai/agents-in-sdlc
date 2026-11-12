---
title: "Exercício 1 - Instruções personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Modo de agente →][next-lesson]

O contexto é essencial ao trabalhar com IA generativa. Se uma tarefa precisa ser realizada de determinada maneira ou o Copilot precisa conhecer informações adicionais, disponibilize esse contexto. Os [arquivos de instruções][instruction-files] fornecem orientações sobre a geração de código.

Neste exercício, você vai:

- explorar como o contexto específico do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio das instruções do repositório e de arquivos associados a caminhos.
- gerar a primeira parte dos dados para a filtragem — um helper de editoras — usando as instruções atuais.
- adicionar um novo padrão para todo o repositório em `.github/copilot-instructions.md`.
- repetir o mesmo prompt e observar o código gerado seguindo o novo padrão.
- fazer commit das instruções e da parte da filtragem em `main` para que o Copilot use a orientação atualizada no próximo exercício.

> [!CAUTION]
> O código gerado pode não seguir alguns dos padrões definidos, pois o Copilot é não determinístico. O objetivo é observar a tendência de mudança após a atualização das instruções, não obter resultados idênticos.

## Arquivos de instruções

### Cenário

A Tailspin Toys tem diretrizes e requisitos para as práticas de desenvolvimento:

- A camada de dados sempre precisa de testes unitários.
- A interface do usuário (UI) deve usar o modo escuro e ter uma aparência moderna.
- O código deve incluir documentação na forma de comentários TSDoc.
- O início de cada arquivo deve conter um bloco de comentários que explique a finalidade do arquivo.

Com arquivos de instruções, você fornecerá ao Copilot as informações necessárias para realizar o trabalho de acordo com essas práticas.

### Instruções personalizadas

As instruções personalizadas fornecem contexto e preferências ao Copilot para que ele entenda melhor o estilo e os requisitos de codificação. Você pode especificar convenções, bibliotecas e os tipos de comentários a incluir. As instruções podem abranger todo o repositório ou tipos específicos de arquivos e tarefas.

Há dois tipos de arquivos de instruções:

- `.github/copilot-instructions.md`, um único arquivo enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter contexto relevante para a maioria das solicitações, como a pilha tecnológica, uma visão geral do projeto, práticas recomendadas e orientações gerais.
- `.github/instructions/*.instructions.md`, arquivos que podem fornecer diretrizes para linguagens, como TypeScript ou Astro, ou para tarefas específicas, como criar um componente de interface ou novos testes unitários.

> [!NOTE]
> No IDE, os arquivos de instruções são usados para gerar código no Copilot Chat, não para sugestões de conclusão de código ou de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam instruções do repositório e arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também [oferece suporte a arquivos de instruções em outros padrões][custom-instructions-support], como `AGENTS.md` e `CLAUDE.md`.

### Práticas recomendadas para gerenciar arquivos de instruções

Os exemplos do projeto mostram uma abordagem representativa:

- Mantenha `copilot-instructions.md` focado em orientações gerais do projeto, como descrição, estrutura e padrões de codificação.
- Use `*.instructions.md` para arquivos ou tarefas específicos, como testes unitários, componentes Astro e a camada de dados.
- Use linguagem natural e mantenha as instruções claras, com exemplos de código que deve e não deve ser produzido.

Não há uma única maneira certa de criar arquivos de instruções ou de usar IA. Experimente para descobrir o que funciona melhor no seu projeto.

> [!TIP]
> Projetos que usam o GitHub Copilot devem ter um conjunto sólido de arquivos de instruções. Neste projeto há instruções para várias tarefas, incluindo [atualizações de interface][ui-instructions] e [Astro][astro-instructions].
>
> O Copilot também pode ajudar a gerar arquivos de instruções. Cada interface oferece essa opção de uma maneira diferente, como **Configure Chat → Generate Agent Instructions** no VS Code ou `/init` no Copilot CLI. A lição do ambiente em uso explicará como fazer isso quando for relevante.
>
> Para encontrar modelos ou um ponto de partida, explore o [awesome-copilot][awesome-copilot], um repositório com arquivos de instruções, agentes personalizados e outros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explorar os arquivos de instruções do projeto

Leia os arquivos de instruções que acompanham o repositório, no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Observe a descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas sobre **GitHub Actions Workflows**.
3. Explore `.github/instructions`. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md` e observe o campo `applyTo` no frontmatter. Ele define um padrão glob relativo à raiz do repositório; arquivos de teste TypeScript, como `**/*.test.ts`, correspondem a ele.
5. Leia as instruções específicas para criar testes unitários.
6. Abra `.github/instructions/drizzle.instructions.md` e leia a parte final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes do projeto. Esses caminhos são relativos ao arquivo de instruções.

> [!NOTE]
> A seção **Code formatting requirements** de `copilot-instructions.md` descreve os padrões de codificação, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentários nos arquivos.

## Criar um branch para as alterações

Crie um branch para manter as alterações organizadas.

1. Volte ao codespace usado no exercício anterior.
2. Abra um terminal com <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crie e selecione um branch:

   ```bash
   git checkout -b custom-instructions
   ```

## Usar o Copilot Chat antes de atualizar as instruções

> [!TIP]
> **Abrir o Copilot Chat**
>
> Volte ao codespace, abra o painel do Copilot Chat e selecione **New Chat** para iniciar uma conversa limpa. O modo e o modelo variam conforme o exercício; cada etapa especificará as opções necessárias.

Para observar o impacto das instruções personalizadas, envie um prompt com o arquivo de instruções atual. Depois, atualize-o e envie o mesmo prompt novamente.

1. Feche as guias de editor abertas em exercícios anteriores para que o Copilot use apenas o contexto necessário.
2. Abra `src/lib/publishers.ts` para indicar onde o helper deve ficar.
3. Na lista de agentes da visualização Chat, selecione **Agent** para permitir que o Copilot altere arquivos.

   ![Captura de tela do seletor de agente na visualização Chat](../../../_images/shared-chat-mode-selector.png)

4. Envie este prompt:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um helper de acesso a dados que retorne uma lista de todas as editoras, com nome e ID para cada uma. Aplique as alterações nos arquivos.
   ```

5. O Copilot explorará o projeto e aplicará alterações, normalmente no helper e nos testes.
6. Observe que a função proposta tem tipos, recebe um cliente `db` como primeiro argumento e retorna uma matriz tipada de editoras. Essas características vêm das convenções da camada de dados em `.github/instructions/drizzle.instructions.md`, aplicáveis a `src/lib/*.ts`.
7. Observe que o código proposto **não tem** comentários TSDoc nem cabeçalho de comentários no arquivo.

> [!CAUTION]
> Como o Copilot é não determinístico, ele pode adicionar comentários mesmo sem essa orientação. Tudo bem: o objetivo é observar a melhoria de consistência após a atualização das instruções.

## Adicionar um padrão para todo o repositório

O arquivo `.github/copilot-instructions.md` fornece orientações gerais ao Copilot. Atualize os padrões de codificação para melhorar as sugestões.

1. Reabra `.github/copilot-instructions.md`.
2. Localize a seção **Code formatting requirements**, próxima à linha 27. Ela descreve os padrões do projeto, mas ainda não exige documentação no código.
3. Logo abaixo dos padrões existentes, adicione estas linhas:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> Como você viu na lição anterior, as instruções podem ficar no nível do repositório, em `.github/copilot-instructions.md`, ou em arquivos `*.instructions.md` para linguagens, tipos de arquivo e tarefas específicas. O arquivo do repositório é o local adequado para padrões gerais, como a regra de comentários adicionada.

## Repetir o prompt e observar a diferença

1. Volte ao Copilot Chat e selecione **New Chat** para limpar o contexto.
2. Selecione `src/lib/publishers.ts` para que o Copilot se concentre no arquivo correto.
3. Envie o mesmo prompt usado anteriormente:

   ```plaintext
   Crie ou atualize src/lib/publishers.ts com um helper de acesso a dados que retorne uma lista de todas as editoras, com nome e ID para cada uma. Aplique as alterações nos arquivos.
   ```

4. Observe que o arquivo proposto agora começa com um bloco de comentários semelhante a este:

   ```typescript
   /**
    * Helpers de acesso a dados de editoras da plataforma de financiamento coletivo Tailspin Toys.
    * Fornece funções para recuperar informações de editoras do banco de dados.
    */
   ```

5. Observe que a função proposta agora inclui um comentário TSDoc semelhante a este:

   ```typescript
   /**
    * Retorna uma lista de todas as editoras com seus identificadores e nomes.
    *
    * @param db - O cliente do banco de dados Drizzle.
    * @returns Uma promessa que é resolvida com uma matriz de objetos de editoras.
    */
   ```

Você orientou o Copilot a seguir um novo padrão e aplicá-lo ao código que será usado no próximo exercício.

## Fazer commit das instruções e enviar o branch

Os arquivos de instruções são controlados pelo mesmo sistema de controle de versão que os demais arquivos do repositório. Faça commit e envie o branch.

1. Abra um terminal com <kbd>Control</kbd>+<kbd>`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Confirme se as instruções e as alterações do helper estão presentes:

   ```bash
   git status
   ```

3. Prepare e faça commit das instruções e dos arquivos alterados pelo Copilot para criar a base do helper:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # Se git status mostrar outras alterações de suporte (por exemplo, testes), adicione esses arquivos também.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Envie o branch:

   ```bash
   git push -u origin custom-instructions
   ```

## Criar e mesclar um pull request

Com o branch enviado, crie um pull request associado à issue de padrões de documentação do backlog. O Copilot pode encontrar a issue, criar um PR associado e mesclá-lo.

> [!NOTE]
> Este é o primeiro exercício em que o Copilot executa ações no GitHub. O modelo do projeto já conecta as ferramentas do GitHub ao workspace, então não é necessário configurar nada. Na primeira vez que o Copilot usar uma ferramenta, o VS Code poderá solicitar autenticação. Siga as instruções. Você aprenderá como essa conexão funciona — por meio do Model Context Protocol — em outra lição.

1. Abra o Copilot Chat no codespace.
2. Pressione <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir a visualização do Copilot Chat e confirme que **Agent** está selecionado.
3. Peça ao Copilot que encontre a issue das instruções e crie um PR a partir do branch atual, descrevendo também a base do helper de editoras:

   ```plaintext
   Encontre a issue relacionada à atualização do arquivo de instruções. Crie um PR a partir do branch atual, indique que ele fecha essa issue e mencione também a base do helper de editoras para o próximo trabalho de filtragem.
   ```

4. Quando solicitado, revise a ação do GitHub e selecione **Allow** se estiver de acordo.
5. Depois da criação do PR, peça ao Copilot que faça a mesclagem e volte para `main`:

   ```plaintext
   Mescle o PR em main. Depois, volte para main localmente e obtenha o código mais recente.
   ```

6. Quando solicitado, revise as ações do GitHub e os comandos de shell e selecione **Allow** se estiver de acordo.

Você criou e mesclou um pull request com a ajuda do GitHub Copilot.

## Resumo e próximos passos

Você explorou como o Copilot obtém contexto dos arquivos de instruções e usou o Copilot Chat no VS Code para:

- enviar um prompt de geração de código e observar o resultado com as instruções *existentes*.
- adicionar um novo padrão para todo o repositório em `.github/copilot-instructions.md`.
- repetir o prompt e observar o código proposto seguindo o novo padrão.
- fazer commit das instruções e da base do helper em `main` para que o próximo exercício possa continuar o trabalho.

Em seguida, você aplicará essas instruções no [modo de agente][next-lesson] enquanto o Copilot adiciona uma funcionalidade à base de código.

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Instruções pessoais personalizadas para o GitHub Copilot][personal-instructions]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
