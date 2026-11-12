---
title: "练习 1 - 自定义说明（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式人工智能（AI）时，上下文至关重要。如果任务必须以特定方式完成，或者 Copilot 需要了解一些背景信息，就应确保它能访问这些上下文。[说明文件][instruction-files]可提供相关指导，帮助 Copilot 理解不仅要做*什么*，还要*如何*完成。

在本练习中，你将：

- 了解项目上下文、编码准则和文档标准如何通过存储库自定义说明及按路径限定范围的说明文件传递给 Copilot。
- 向 `.github/copilot-instructions.md` 添加一项全存储库适用的新标准。

> [!NOTE]
> 与 VS Code 和 CLI 路径不同，本练习不会比较提示的*前后*效果。Copilot 云智能体会异步处理 GitHub issue，因此很难实时并排展示差异。后续审查云智能体创建的拉取请求时，可以看到说明文件的影响。

## 说明文件

### 场景

Tailspin Toys 和许多开发团队一样，制定了开发实践准则和要求，包括：

- 数据层始终需要单元测试。
- 用户界面（UI）应采用深色模式并具有现代感。
- 应通过 TSDoc 文档注释为代码添加文档。
- 每个文件开头都应添加一段注释，说明该文件的用途。

使用说明文件，可以让 Copilot 获取正确信息，按照上述实践完成任务。

### 自定义说明

自定义说明可为 Copilot 提供上下文和偏好，帮助它理解你的编码风格和需求。可以指定编码约定、库，以及希望采用的注释风格。既可以为整个存储库创建说明，也可以针对特定文件类型创建说明，提供任务级上下文。

说明文件分为两类：

- `.github/copilot-instructions.md`：面向整个存储库的单个说明文件，会随该存储库的**每个**请求发送给 Copilot。此文件应包含适用于大多数聊天或 CLI 请求的项目级信息，例如所用技术栈、项目概述、最佳实践和其他全局指导。
- `.github/instructions/*.instructions.md`：可针对特定任务或文件类型创建，例如为 TypeScript 或 Astro 提供指导，或说明如何创建 UI 组件或一组单元测试。

> [!NOTE]
> 在集成开发环境（IDE）中，说明文件仅用于 Copilot Chat 生成代码，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云智能体在生成代码时，都会使用存储库级说明文件以及带有 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他标准的说明文件][custom-instructions-support]，包括 `AGENTS.md` 和 `CLAUDE.md`。

### 管理说明文件的最佳实践

全面讨论如何创建说明文件超出了本工作坊的范围。示例项目展示了一种有代表性的做法，主要原则如下：

- 让 `copilot-instructions.md` 聚焦于项目级指导，例如项目简介、结构和全局编码标准。
- 使用 `*.instructions.md` 为特定文件类型（例如单元测试、Astro 组件和数据层）或特定任务提供指导。
- 使用自然语言，保持说明清晰，并提供代码应如何编写或不应如何编写的示例。

说明文件没有唯一的正确写法，AI 的使用方式也不止一种。通过实践，你会找到适合项目的方法。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应有一套完善的说明文件。浏览本项目中的文件时，会看到它们涵盖多种任务，包括 [UI 更新][ui-instructions]和 [Astro][astro-instructions]。
>
> Copilot 也可以帮助生成说明文件。各个界面的入口不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。对应的课程会在相关位置介绍。
>
> 需要模板或起点？可以浏览 [awesome-copilot][awesome-copilot]，其中收集了说明文件、自定义智能体和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 探索项目中的自定义说明文件

先阅读存储库附带的说明文件，其中包括核心文件 `copilot-instructions.md` 和一组面向不同任务的 `*.instructions.md` 文件。可以在编辑器或 GitHub Web UI 中打开这些文件。

1. 打开 `.github/copilot-instructions.md`。
2. 浏览文件中的项目简介和 **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** 等部分。还要查看 **Code standards** 下的 **GitHub Actions Workflows** 嵌套指导。这些内容适用于与 Copilot 的各种交互。
3. 打开 `.github/instructions` 文件夹并浏览，查看针对 Astro 文件、Drizzle 数据层、测试等内容的说明。
4. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo` 字段，它设置了一个相对于存储库根目录的 glob，用于确定适用文件。此处，匹配 `**/*.test.ts` 的 TypeScript 测试文件都会匹配。
5. 查看该文件中针对本项目单元测试的具体说明。
6. 最后，打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部。查看它指向的其他说明文件（例如 `unit-tests.instructions.md`）和项目文件。这样可以将较大的说明集拆分成更小、可复用的文件，并为 Copilot 提供示例。（这些路径相对于说明文件所在位置，而不是存储库根目录。）

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但目前没有要求在代码中编写文档。接下来会添加 TSDoc 文档注释和文件注释头规则。

## 添加新的存储库级标准

接下来只需编辑一次：添加一项项目级规则，要求在代码中使用 TSDoc 文档注释和文件级注释头。云智能体之后处理分配给它的 issue 时会遵循这项规则。

编辑前先创建工作分支。云智能体会读取 issue 目标分支中的说明，但仍应妥善提交自己的更改。

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。补充存储库编码标准，可以改善代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分（应在第 27 行附近）。查看其中记录的编码标准；目前没有代码文档规则，这也是生成的 helper 没有文档注释的原因。
3. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，说明文件可以放在存储库级文件 `.github/copilot-instructions.md` 中，提供全局指导；也可以放在 `*.instructions.md` 文件中，指导特定语言、文件类型或任务。刚添加的文档注释规则属于项目级标准，应放在存储库级文件中。

## 提交、推送并合并说明更新

云智能体会从 issue 目标分支读取说明。下一练习中，Copilot 会从 `main` 分支创建分支，因此必须先将说明更改合并到 `main`，云智能体才能使用。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求并合并。之后，云智能体处理本路径后续练习分配的 issue 时，就会读取这些说明。

> [!TIP]
> 如果希望在本工作坊中直接使用 `main`，可以跳过分支步骤并直接提交到 `main`。此处创建分支是为了模拟真实项目中的工作方式。

## 总结和后续步骤

你了解了 Copilot 如何从项目说明文件中获取上下文，并向 `.github/copilot-instructions.md` 添加了一项全存储库适用的新标准。后续审查云智能体创建的拉取请求时，可以看到它如何遵循此标准。

接下来，[将第一个 issue 分配给 Copilot 云智能体][next-lesson]。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [为 Copilot 编写更好自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot——说明文件及其他资源][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
