---
title: "Exercício 1 - Instruções personalizadas (agente de nuvem)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lição anterior: Pré-requisitos][previous-lesson] · [Próxima lição: Agente de nuvem do Copilot →][next-lesson]

O contexto é essencial ao trabalhar com inteligência artificial (IA) generativa. Se uma tarefa precisa ser realizada de determinada maneira ou o Copilot precisa conhecer informações de contexto, disponibilize essas informações. Os [arquivos de instruções][instruction-files] fornecem orientações para que o Copilot entenda não apenas *o que* você quer, mas também *como* realizar o trabalho.

Neste exercício, você vai:

- explorar como o contexto do projeto, as diretrizes de codificação e os padrões de documentação chegam ao Copilot por meio das instruções do repositório e de arquivos de instruções associados a caminhos.
- adicionar um novo padrão para todo o repositório em `.github/copilot-instructions.md`.

> [!NOTE]
> Diferentemente dos ambientes do VS Code e da CLI, aqui você não fará uma comparação entre prompts antes e depois. O agente de nuvem do Copilot trabalha de forma assíncrona em issues do GitHub, então é mais difícil demonstrar o impacto em tempo real. Você verá a influência do arquivo de instruções mais adiante, ao revisar os pull requests gerados pelo agente.

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

- `.github/copilot-instructions.md`, um único arquivo enviado ao Copilot em **todas** as solicitações do repositório. Ele deve conter informações sobre o projeto relevantes para a maioria das solicitações, como a pilha tecnológica, uma visão geral do que está sendo desenvolvido, práticas recomendadas e orientações gerais.
- `.github/instructions/*.instructions.md`, arquivos que podem fornecer diretrizes para linguagens específicas, como TypeScript ou Astro, ou para tarefas, como criar componentes de interface ou testes unitários.

> [!NOTE]
> No IDE, os arquivos de instruções são usados para gerar código no Copilot Chat, não para sugestões de conclusão de código ou de próxima edição.
>
> O Copilot Chat, o Copilot CLI e o agente de nuvem do Copilot usam instruções do repositório e arquivos `*.instructions.md` com frontmatter `applyTo` ao gerar código.
>
> O Copilot também [oferece suporte a arquivos de instruções em outros padrões][custom-instructions-support], como `AGENTS.md` e `CLAUDE.md`.

### Práticas recomendadas para gerenciar arquivos de instruções

Os exemplos do projeto mostram uma abordagem representativa para criar arquivos de instruções:

- Mantenha `copilot-instructions.md` focado em orientações para o projeto, como descrição, estrutura e padrões gerais de codificação.
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

Leia os arquivos de instruções que acompanham o repositório — um `copilot-instructions.md` principal e vários arquivos `*.instructions.md` para diferentes tarefas. Abra-os no editor ou na interface Web do GitHub.

1. Abra `.github/copilot-instructions.md`.
2. Observe a descrição do projeto e seções como **Agent notes**, **Code standards**, **Scripts** e **Repository Structure**. Em **Code standards**, observe as orientações aninhadas sobre **GitHub Actions Workflows**. Essas informações se aplicam às interações com o Copilot.
3. Explore a pasta `.github/instructions`. Há instruções para arquivos Astro, a camada de dados Drizzle, testes e outros tópicos.
4. Abra `.github/instructions/unit-tests.instructions.md` e observe o campo `applyTo` no frontmatter. Ele define um padrão glob relativo à raiz do repositório; neste caso, arquivos de teste TypeScript como `**/*.test.ts` correspondem ao padrão.
5. Leia as instruções específicas para criar testes unitários neste projeto.
6. Abra `.github/instructions/drizzle.instructions.md` e leia a parte final. Observe os links para outros arquivos de instruções, como `unit-tests.instructions.md`, e para arquivos existentes do projeto. Esses caminhos são relativos ao arquivo de instruções.

> [!NOTE]
> A seção **Code formatting requirements** de `copilot-instructions.md` documenta os padrões de codificação do projeto, mas ainda não exige documentação no código. Nas próximas etapas, você adicionará regras para comentários TSDoc e cabeçalhos de comentários nos arquivos.

## Adicionar um padrão para todo o repositório

Agora, você adicionará ao projeto uma regra que exige comentários TSDoc e um cabeçalho de comentário no início dos arquivos. O agente de nuvem usará essa regra nas issues atribuídas mais adiante.

Antes de editar o arquivo, crie um branch. O agente de nuvem lê as instruções do branch de destino da issue, mas você fará um commit organizado das alterações.

1. No terminal do codespace, crie e selecione um novo branch:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. Abra `.github/copilot-instructions.md` e localize a seção **Code formatting requirements**, próxima à linha 27.
3. Logo abaixo dos padrões existentes, adicione estas linhas:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Salve `copilot-instructions.md`.

> [!TIP]
> As instruções podem ficar no nível do repositório, em `.github/copilot-instructions.md`, ou em arquivos `*.instructions.md` para linguagens, tipos de arquivo e tarefas específicas. O arquivo do repositório é o local adequado para padrões gerais, como a regra de comentários adicionada.

## Fazer commit, enviar e mesclar a atualização das instruções

O agente de nuvem lê as instruções do branch de destino da issue. No próximo exercício, ao atribuir uma issue ao Copilot, ele criará um branch a partir de `main`. Portanto, as instruções precisam ser mescladas em `main` para que o agente as use.

1. Prepare e faça commit da alteração:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envie o branch:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. No github.com, abra um pull request de `custom-instructions-cloud` para `main` e faça a mesclagem.

> [!TIP]
> Se preferir trabalhar diretamente em `main` neste workshop, ignore as etapas do branch e faça commit diretamente em `main`. O uso do branch permite praticar um fluxo mais parecido com o trabalho em um projeto real.

## Resumo e próximos passos

Você explorou como o Copilot obtém contexto dos arquivos de instruções e adicionou um padrão para todo o repositório em `.github/copilot-instructions.md`. Você verá esse padrão nos pull requests que o agente de nuvem criar nas próximas lições.

Em seguida, você [atribuirá sua primeira issue ao agente de nuvem do Copilot][next-lesson].

## Recursos

- [Arquivos de instruções para personalizar o GitHub Copilot][instruction-files]
- [Práticas recomendadas para criar instruções personalizadas][instructions-best-practices]
- [5 dicas para escrever instruções melhores para o Copilot][copilot-instructions-five-tips]
- [Awesome Copilot — coleção de arquivos de instruções e outros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
