---
title: "Lição 12 - Implantar o site com o GitHub Pages"
description: "Use o aplicativo GitHub Copilot para configurar um fluxo de trabalho do Pages, revisar o pull request e verificar o Space Quiz publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Dê ao Space Quiz um endereço público implantando-o com o GitHub Pages. O Copilot pode preparar o fluxo de trabalho e orientar a implantação, mas cabe a você revisar as mudanças e confirmar que o site está no ar.

Nesta lição, você vai:

- pedir ao Copilot para configurar a implantação no GitHub Pages.
- revisar o fluxo de trabalho e o pull request antes da mesclagem.
- acompanhar a implantação e verificar o site publicado.

## Cenário

O Space Quiz já está em um repositório do GitHub, mas as pessoas ainda precisam de uma maneira simples de experimentá-lo. Publicar o site de arquivo único com o GitHub Pages o disponibiliza em um endereço da Web (URL) público, sem adicionar um servidor ou dependência de tempo de execução (runtime).

## Peça ao Copilot para implantar o site

O prompt a seguir orienta o Copilot a configurar e verificar a implantação do repositório `space-quiz` no GitHub Pages.

1. Envie este prompt:

   ```plaintext
   Habilite o GitHub Pages para este repositório. Crie um fluxo de trabalho do GitHub Actions que compile o site, se necessário, e o implante no GitHub Pages. Se ainda não houver um README, adicione um que descreva o aplicativo e explique como executá-lo localmente. Crie um pull request com essas mudanças e faça a mesclagem depois que as verificações obrigatórias forem aprovadas. Acompanhe a implantação até que ela seja concluída com êxito e informe a URL final do site publicado. Se você não tiver permissão para habilitar o Pages ou mesclar o pull request, diga exatamente o que preciso aprovar ou fazer; não informe que a tarefa foi concluída até que o site esteja no ar.
   ```

![Diagrama em três etapas: um pull request do space-quiz mesclado; uma execução bem-sucedida de Deploy website no GitHub Actions, com as etapas Build website, Upload artifact e Deploy to Pages; e o Space Quiz publicado em yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

> [!WARNING]
> Este prompt pede ao agente que crie e mescle um pull request e altere as configurações do Pages do repositório. Revise as diferenças, as permissões de implantação e todas as solicitações de aprovação do GitHub antes de continuar.

## Revise o fluxo de trabalho e verifique a implantação

A revisão das mudanças e da execução de implantação confirma que o site está pronto para ser considerado concluído.

1. Confirme se o README foi adicionado somente quando o repositório ainda não tinha um.
2. Revise as mudanças do pull request, incluindo as etapas de compilação e implantação do fluxo de trabalho.
3. Faça a mesclagem somente depois que as verificações obrigatórias do pull request forem aprovadas.
4. Acompanhe a execução de implantação do GitHub Actions até que ela seja concluída com êxito.
5. Abra a URL informada e confirme se o Space Quiz carrega.
6. Se o agente não puder habilitar o Pages ou mesclar o pull request, siga as instruções específicas que ele fornecer.

Não considere a tarefa concluída até que a implantação seja bem-sucedida e o site esteja carregado.

## Resumo e próximos passos

Agora o Space Quiz está disponível como um site publicado, e você verificou a implantação em vez de confiar apenas no relato do agente. Continue para [a Lição 13: Revisão e próximos passos][next-lesson].

[next-lesson]: ../13-review/
