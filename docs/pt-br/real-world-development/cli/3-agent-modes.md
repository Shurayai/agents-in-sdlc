---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Use Plan para combinar uma abordagem, Autopilot para implementar a filtragem com base em uma issue e Interactive para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Começamos adicionando uma pequena funcionalidade ao projeto, mas mudanças maiores exigem um processo mais robusto. O GitHub Copilot CLI foi criado para trabalhar com o fluxo de desenvolvimento existente da organização e ajudar a construir as soluções certas da maneira certa. Nesta e nas próximas lições, você seguirá um processo típico de desenvolvimento orientado por agentes: partirá de uma issue para criar uma funcionalidade, verificará o código e o comportamento e, por fim, fará a mesclagem no projeto.

> [!NOTE]
> Você usará a mesma conversa e o mesmo branch durante o fluxo de trabalho da funcionalidade. Em geral, seriam usados branches ou PRs diferentes para tipos distintos de alteração, mas aqui faremos um atalho para focar nos conceitos principais.

Nesta lição, você vai:

- iniciar uma conversa do Copilot com base em uma issue do GitHub.
- definir os requisitos no modo Plan.
- implementar a funcionalidade no modo Autopilot.
- revisar o código.
- validar a funcionalidade manualmente em um navegador encaminhado.

Ao continuar esse trabalho, você atualizará as instruções do repositório, personalizará a skill existente `quality-checks`, adicionará validação com MCP, criará um agente de QA e abrirá o PR da funcionalidade.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam filtrar os jogos por categoria e editora. A issue do backlog descreve a funcionalidade, mas detalhes como combinar categorias precisam ser definidos antes de começar a programar. Você usará o modo Plan para tomar essas decisões e, em seguida, autorizará uma implementação com escopo definido no modo Autopilot.

## Contexto

Usar agentes de programação com IA não muda os fundamentos do desenvolvimento. Na verdade, eles se tornam ainda mais importantes. Um fluxo comum entre desenvolvedores é:

1. Começar por uma issue registrada que descreva o trabalho.
2. Criar um plano do que precisa ser implementado.
3. Implementar e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar um pull request (PR).
7. Depois da revisão do código e da aprovação da integração contínua, mesclar as alterações.

> [!NOTE]
> Os detalhes exatos variam entre equipes e organizações, mas a maioria dos fluxos segue alguma variação desse processo.

Esse processo ajuda a garantir que o código gerado por IA atenda aos requisitos e passe pelo mesmo nível de revisão que o código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla o nível de autonomia do agente. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre os modos:

- **Interactive**: você e o agente trabalham em conjunto. O agente sugere mudanças e aguarda sua orientação antes de continuar.
- **Plan**: o agente cria um plano primeiro e não pode editar os arquivos do projeto.
- **Autopilot**: o agente trabalha de forma autônoma, escreve código, executa testes e itera até considerar a tarefa concluída.

Comece no modo Plan, revise o plano e depois use Autopilot para implementá-lo.

## Começar pela issue

Antes de iniciar o trabalho de filtragem, volte ao codespace e confirme que o repositório e o terminal estão prontos.

1. Volte ao codespace. Se estiver parado, reinicie-o antes de continuar.
2. Confirme se o PR das avaliações por estrelas foi mesclado.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Atualize `main` e crie um branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a guia **Issues**.
7. Pressione <kbd>A</kbd> para exibir todas as issues.
8. Use as setas para destacar a issue **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e voltar à guia **Session**.

Observe que o prompt agora começa com `#7` (ou um número semelhante). O caractere `#` permite adicionar ao contexto uma issue ou um pull request do GitHub.

## Planejar a filtragem

O planejamento permite definir a abordagem antes de delegar uma funcionalidade ou tarefa ao Copilot. Para trabalhos complexos, vale a pena planejar. Alterne para o modo Plan e peça ao Copilot que crie o plano.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para mudar para o modo Plan. Confirme que o indicador abaixo do prompt exibe **Plan**.
2. Depois da referência à issue adicionada na etapa anterior, digite este prompt:

   ```plaintext
   Crie um plano para implementar esta funcionalidade.
   ```

O Copilot explorará o projeto e determinará a melhor abordagem.

3. O Copilot pode perguntar como a filtragem deve funcionar. Responda de acordo com suas preferências.
4. Quando o plano estiver pronto, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandi-lo.
5. Percorra o plano e revise-o.
6. Peça ao Copilot que altere qualquer parte que não corresponda às suas decisões.

## Aprovar o Autopilot

Com o plano escrito e revisado, implemente-o usando o modo Autopilot. Esse modo permite que o Copilot itere até considerar o trabalho concluído.

1. Selecione **Accept plan and build on autopilot (recommended)** ou a opção equivalente na versão instalada.
2. Confirme que o indicador abaixo do prompt exibe **Autopilot**.
3. Acompanhe o Copilot enquanto ele segue o plano, gera código e executa testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, portanto revise o plano antes. Se o Copilot informar que faltam dependências ou que há conflito de porta, resolva o problema de configuração antes de considerar as verificações concluídas.

## Revisar e verificar a implementação

Assim como qualquer outro código, o código gerado precisa ser revisado antes da mesclagem. Revise as mudanças e execute o site para conferir o resultado.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interactive. Confirme que o indicador não exibe **Plan** nem **Autopilot**.
2. Digite `/diff` e inspecione a implementação da filtragem e os testes.
3. Compare o resultado com a issue e com as decisões tomadas no planejamento.
4. Depois da revisão, pressione <kbd>Esc</kbd> para sair da visualização de diferenças.
5. Revise a saída das verificações do projeto e peça ao Copilot que corrija eventuais falhas.

## Explorar a nova funcionalidade

O código parece correto, mas será que funciona? Peça ao Copilot que inicie o aplicativo e abra o site pela porta encaminhada do Codespaces.

1. Peça ao Copilot que inicie o aplicativo:

   ```plaintext
   Inicie o aplicativo para que eu possa testar a filtragem no navegador. Informe a URL e deixe o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Teste os filtros por categoria, por editora e as combinações definidas no plano.
4. Confirme se o comportamento de redefinição e de resultados vazios corresponde à issue e às decisões tomadas.
5. Volte ao codespace e peça ao Copilot que encerre o servidor de desenvolvimento iniciado por ele.

## Resumo e próximos passos

Você usou diferentes modos de conversa para criar e revisar uma funcionalidade. Nesta lição, você:

- iniciou uma conversa do Copilot com base em uma issue do GitHub.
- definiu os requisitos no modo Plan.
- implementou a funcionalidade no modo Autopilot.
- revisou o código.
- validou a funcionalidade manualmente em um navegador encaminhado.

Em seguida, você [orientará o Copilot com instruções personalizadas][next-lesson] para que o código siga as práticas documentadas.

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
