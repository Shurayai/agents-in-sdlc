---
title: "练习 2 - 使用 Copilot 智能体模式添加新功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行一些操作，例如运行测试。开发者通常需要找到所有相关文件、进行更改、运行测试、调试、找出遗漏的文件并再次修改，工作往往会不断重复。

Copilot 智能体模式可以帮助处理这类工作。

Copilot 智能体模式可以在集成开发环境（IDE）中更自主地工作。它会先探索现有项目结构，再执行必要的更新、运行测试等任务，并自动修复发现的问题。现在看看如何使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云智能体的名称相似，但适用于两种不同的体验。智能体模式在 IDE 中执行任务，支持快速反馈和交互。云智能体则像团队成员一样异步工作，通过 issue 和拉取请求与你协作。

在本练习中，你将了解如何：

- 使用 Copilot 智能体模式探索项目、查找相关文件并协调多文件更改。
- 使用 GitHub Copilot 智能体模式跨用户界面和数据层实现新功能。
- 在将更改合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

## 场景

游戏列表不断增长，因此需要允许用户按类别和发布商筛选。上一练习已添加 publishers helper，现在将使用 Copilot 智能体模式完成数据层、用户界面和测试方面的工作。

## 运行 Tailspin Toys 网站

更改代码前，先体验 Tailspin Toys 网站，了解它目前的功能。

这是一个以开发者为主题、为棋盘游戏提供众筹的平台。用户可以浏览游戏列表并查看详情。网站是一个 Astro 应用，会在构建时将页面渲染为静态超文本标记语言（HTML）。页面通过 Drizzle 对象关系映射（ORM）在 frontmatter 中直接查询本地 SQLite 数据库，没有单独的后端应用程序编程接口（API）或客户端用户界面（UI）框架。可复用的数据访问 helper 位于 `src/lib/`，交互功能则使用少量作用范围明确的 Astro `<script>` 和标准文档对象模型（DOM）API 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单个 Astro 开发服务器。按以下步骤在 GitHub Codespace 中运行：

1. 返回 Codespace。上一练习结束后，当前分支应为 `main`。
2. 按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux），在 Codespace 中打开新终端。
3. 更新 main，并为过滤功能创建新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，会显示类似以下内容的横幅，其中包含统一资源定位符（URL）：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果出现提示，询问是否在浏览器窗口中打开 `http://localhost:4321`，请选择 **x** 将其关闭。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后选择终端中的 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中，从终端选择 localhost URL 会自动将你转到 `https://<your-codespace-name>-4321.app.github.dev/`。这是连接到 Codespace 的私有隧道，Web 服务器此时正在 Codespace 中运行。

### 浏览网站

网站启动后，可以浏览以下主要功能：

- **主页**：显示游戏名称、图片和说明。
- **游戏详情页**：选择游戏后会打开详情页，其中包含游戏名称、说明、发布商和类别等信息。

## 使用 Copilot 浏览待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。模式和模型的选择因练习而异；相关步骤会在需要时说明。

网站已有基础功能，但还需要添加更多能力。先查看待办事项。使用项目模板时，系统已自动创建了一组 issue；请 GitHub Copilot 列出这些事项。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。Agent 智能体可以自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本工作坊作者并非推荐某一种模型。编写本工作坊时使用了 Claude Sonnet 4.5，因此将其列入说明，希望让代码建议相对一致，提供良好的体验。不过，大语言模型（LLM）具有概率性，你可能会看到与示例不同的建议。这是正常现象。

> [!NOTE]
> 由于结果具有概率性，Copilot 可能会使用不同的模型上下文协议（MCP）命令，但仍应能完成任务。

3. 发送以下提示，请 Copilot 查看 issue 待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue**，运行列出所有 issue 的命令。
5. 查看生成的 issue 列表。

Copilot 还会根据它认为对用户最有用的程度，为待办事项排序。

## 查看说明文件

让智能体生成代码前，先查看用于向 Copilot 提供上下文的说明文件。本练习将使用[用户界面（UI）说明文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)，其中介绍了为网站添加功能时应采用的方法。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看其中关于添加功能的整体指导，包括：
   - 项目架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向各类文件专用说明的链接，包括：
     - Astro。
     - Tailwind CSS。
     - Drizzle。

> [!TIP]
> 说明文件可以引用其他说明文件和项目文件。路径相对于说明文件所在位置。这样可以复用说明，将复杂说明拆分成更易管理的部分，并提供示例和模板。

## 实现过滤功能

要完成过滤功能，至少需要对应用进行三项不同的更新：

- 在数据层（`src/lib/`）添加或完善剩余过滤逻辑。
- 添加或更新过滤行为测试。
- 更新游戏列表页，添加过滤用户界面。

此外，合并代码前必须运行并通过测试。Copilot 智能体模式可以执行这些任务。

1. 继续当前 Copilot 对话，或选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，然后选择 `ui` 说明文件。

   ![选择 UI 说明文件的示例](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选中 **Agent**。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示，请 Copilot 根据待办事项中的相关 issue 实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 如何先探索项目并查找相关文件。它应会找到数据层 helper、用户界面和测试，然后修改文件并运行测试。

   ![Copilot 正在探索项目文件](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多个任务，例如探索项目、修改文件和运行测试。根据任务和代码库的复杂程度，这可能需要几分钟。期间编辑器中可能会出现 **Keep** 和 **Undo** 按钮。Copilot 完成后，所有更改都会显示 **Keep** 或 **Undo** 按钮；工作进行时无需选择。

7. Copilot 提示运行测试时，选择 **Continue**。

   ![Copilot Chat 面板中的对话框，询问是否运行测试](../../../_images/ex3-agent-mode-run-tests.png)

8. Copilot 可能会暂停，或在处理中遇到测试失败。这没有关系。它会在生成代码和运行测试之间迭代，直到完成任务且未检测到错误。

   ![已完成的 Copilot 智能体模式 Chat 会话](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，查找潜在问题。

> [!CAUTION]
> 务必审查 Copilot 或其他人工智能（AI）工具生成的代码。

10. 返回正在运行网站的浏览器，体验新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

本练习中，你使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加了新功能。具体来说，你：

- 使用 Copilot 智能体模式跨用户界面和数据层实现了新功能。
- 使用 Copilot 智能体模式探索项目、查找相关文件并协调多文件更改。
- 在合并到代码库前审查了 Copilot 智能体模式生成的更改和测试。

接下来，[使用 Playwright MCP 服务器测试功能][next-lesson]，然后创建拉取请求。

### 额外探索练习——实现分页

随着游戏列表不断增长，网站将需要分页功能。可以运用本练习中学到的技能，请 Copilot 更新网站以实现分页。规划实现方式时，考虑以下事项：

1. 遵循现有最佳实践，包括使用已有说明文件。
2. 确定分页方式，例如是否允许用户选择页面大小，还是使用固定页面大小。
3. 编写提示时提供足够指导，让 Copilot 按预期实现功能。
4. 如有需要，通过后续提示和补充上下文进行迭代。这是与 Copilot 协作时的正常流程。

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
