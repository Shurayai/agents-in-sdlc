---
title: "练习 1 - 自定义说明（VS Code）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：智能体模式 →][next-lesson]

使用生成式人工智能（AI）时，上下文至关重要。如果任务必须以特定方式完成，或者 Copilot 需要了解一些背景信息，就应确保它能访问这些上下文。可以通过多种方式向 Copilot 提供具体上下文，其中一种主要方式是使用[说明文件][instruction-files]指导代码生成。

在本练习中，你将：

- 了解项目上下文、编码准则和文档标准如何通过存储库自定义说明及按路径限定范围的说明文件传递给 Copilot。
- 在现有说明生效时生成过滤功能的第一部分数据访问代码（publishers helper）。
- 向 `.github/copilot-instructions.md` 添加一项全存储库适用的新标准。
- 再次运行相同提示，观察生成的代码如何采用新标准。
- 将说明更新和过滤功能数据部分提交到 `main`，供下一练习使用。

> [!CAUTION]
> 生成的代码可能不完全遵循设定的标准。Copilot 具有概率性而非确定性。本练习的目标是观察更新说明后行为的一致性变化，而不是要求输出逐字符相同。

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

## 为更改创建分支

遵循良好实践，为本次更改创建分支。

1. 返回上一练习中使用的 Codespace。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
3. 创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions
   ```

## 更新说明前使用 Copilot Chat

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。模式和模型的选择因练习而异；相关步骤会在需要时说明。

为了观察自定义说明的影响，先在当前说明生效时发送提示。稍后会更新说明文件，再发送相同提示进行比较。

1. 关闭之前练习中打开的编辑器选项卡，避免 Copilot 获取不需要的上下文。
2. 打开 `src/lib/publishers.ts`，让 Copilot 知道 helper 应放置的位置。
3. 在 Chat 视图的智能体下拉列表中选择 **Agent**，以便 Copilot 修改文件。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 发送以下提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot 会探索项目并应用代码更新，通常会同时修改 helper 文件及其测试。
6. 查看建议的 helper：它应是一个带类型的函数，第一个参数接收 `db` 客户端，并返回带类型的 publishers 数组。这遵循 `.github/instructions/drizzle.instructions.md` 中的数据层约定，该文件适用于 `src/lib/*.ts`。
7. 注意建议的代码**缺少** TSDoc 文档注释和文件级注释头。

> [!CAUTION]
> Copilot 具有概率性，即使没有明确要求，也可能添加文档注释。这种情况也没关系；本练习要观察的是更新说明后行为的一致性变化。

## 添加新的存储库级标准

如前所述，`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。补充存储库编码标准，可以改善代码建议。

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

## 再次运行提示并观察变化

1. 返回 Copilot Chat 并选择 **New Chat**，清空当前对话上下文。
2. 单击 `src/lib/publishers.ts`，让 Copilot 聚焦于正确的文件。
3. 再次发送相同提示：

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 查看建议的文件，确认开头新增了类似以下注释块的内容：

   ```typescript
   /**
    * Tailspin Toys 众筹平台的 publisher 数据访问辅助函数。
    * 提供用于从数据库检索 publisher 信息的函数。
    */
   ```

5. 确认建议的函数现在包含类似以下 TSDoc 注释：

   ```typescript
   /**
    * 返回所有 publisher 的列表及其 id 和 name。
    *
    * @param db - Drizzle 数据库客户端。
    * @returns 一个 Promise，解析为 publisher 对象数组。
    */
   ```

你已引导 Copilot 遵循新的项目标准，并将其应用于下一练习会继续扩展的实际代码。

## 提交说明更新并推送分支

说明文件与存储库中的其他资源一样，也需要通过源代码管理进行维护。现在提交并推送分支。

1. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开新终端。
2. 在终端中运行以下命令，确认说明更新和 helper 更改均已存在：

   ```bash
   git status
   ```

3. 在终端中暂存并提交说明更新以及 Copilot 为 helper 基础所更改的所有文件：

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # 如果 git status 显示还有其他相关更新（例如测试），也要添加这些文件。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. 将分支推送到存储库：

   ```bash
   git push -u origin custom-instructions
   ```

## 创建并合并拉取请求

分支已推送，接下来创建拉取请求，并将它关联到待办事项中的文档标准 issue。Copilot 已连接到项目的 GitHub 工具，可以查找 issue、创建关联的拉取请求（PR）并合并。

> [!NOTE]
> 这是第一次让 Copilot 代表你在 GitHub 上操作。项目模板已配置 GitHub 工具，无需额外设置。Copilot 首次使用工具时，VS Code 可能会提示你登录 GitHub。按提示授权即可。后续练习会介绍这种连接所用的模型上下文协议（MCP）。

1. 在 Codespace 中打开 Copilot Chat。
2. 按 <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd>（Windows/Linux）打开 Copilot Chat 视图，并确保智能体选择器中选中 **Agent**。
3. 请 Copilot 查找与更新说明文件相关的 issue，并从当前分支创建 PR，说明其中既有说明更新，也有用于后续过滤工作的 publishers helper 基础：

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. 等待 Copilot 查找 issue 并创建 PR。
5. 如果 Copilot 提示允许它代表你执行 GitHub 操作，请审查命令，并酌情选择 **Allow**。
6. PR 创建后，使用以下提示请求 Copilot 合并 PR 并将本地分支切回 main：

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. 如果 Copilot 提示允许它代表你执行 GitHub 操作和 shell 命令，请审查命令，并酌情选择 **Allow**。

你已借助 GitHub Copilot 创建并合并拉取请求。

## 总结和后续步骤

本练习中，你：

- 了解了项目上下文、编码准则和文档标准如何通过说明文件传递给 Copilot。
- 在现有说明生效时使用提示生成了过滤功能的数据访问代码（publishers helper）。
- 向 `.github/copilot-instructions.md` 添加了一项全存储库适用的新标准。
- 再次运行了相同提示，并观察生成的代码如何采用新标准。
- 将说明更新和 helper 基础提交到了 `main`，供下一练习使用。

接下来，让 Copilot 在代码库中添加新功能，并在[智能体模式][next-lesson]中应用这些说明。

## 资源

- [GitHub Copilot 自定义说明文件][instruction-files]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [为 Copilot 编写更好自定义说明的 5 个技巧][copilot-instructions-five-tips]
- [GitHub Copilot 个人自定义说明][personal-instructions]
- [Awesome Copilot——说明文件及其他资源][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
