---
title: "练习 2 - GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义说明][previous-lesson] |
|:--|

几乎所有组织都面临技术债务，例如尚未解决的安全问题、需要更新的旧代码，或因缺少时间而长期搁置的功能请求。GitHub Copilot 云智能体可以自主执行更新代码、添加功能等任务。完成后，它会创建草稿拉取请求，供开发者审查。这样可以将繁琐任务交给智能体处理，加快开发流程，让开发者专注于更重要的工作。

本练习将介绍如何使用 Copilot 云智能体：

- 自定义代码生成环境。
- 确保安全地执行操作。
- 了解明确界定 issue 范围的重要性。
- 将 issue 分配给 Copilot。

## 场景

Tailspin Toys 有一些技术债务需要处理。最初承接网站建设的团队没有留下足够的文档。首先，团队希望为应用程序中所有导出的函数添加 TSDoc 文档注释。

此外，设计团队希望改进游戏发现体验：在每款游戏的详情页上显示同类别的其他游戏，让用户可以继续浏览。团队目前不要求完善的实现，只需要一个可用于用户体验验收测试的版本。此需求目前是一个阻塞项，但优先级低于其他 issue。

这类任务很容易被不断延后。将其分配给 Copilot 云智能体后，它可以在后台异步处理，开发者则继续其他工作，稍后再回来审查结果。

## 了解 GitHub Copilot 云智能体

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以像开发者一样在后台处理任务。你可以通过多种方式启动任务，例如[将 GitHub issue 分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配后，Copilot 会创建草稿拉取请求以跟踪进度、准备环境并开始处理任务。任务进行期间或完成后，都可以查看 Copilot 会话。提议的解决方案准备好供审查时，Copilot 会在拉取请求中通知你。

## 明确界定说明和任务范围的重要性

GitHub Copilot 并非魔法工具，不能替代思考。即使看似简单的操作，也可能涉及许多细节，因此[为 Copilot 云智能体明确界定任务范围][cloud-agent-best-practices]很重要。把它当作人工智能（AI）结对编程伙伴：分阶段工作、学习、试验并不断调整。引入生成式 AI 并不会改变软件开发的基本原则。

## 查看此存储库中的自定义说明

前面的练习介绍了自定义说明及其如何指导 Copilot。如果已经完成相关动手练习，就会看到 `.github/copilot-instructions.md` 的作用；如果还没有，现在可以快速查看。分配任务前，在 GitHub 存储库或已启动的 Codespace 中查看以下说明文件，以便稍后识别它们的影响：

1. 在存储库的 GitHub 网页用户界面（UI）中打开 `.github/copilot-instructions.md`；如果已启动 Codespace，也可以在那里打开。查看 **Code standards** 部分，尤其是 TypeScript 约定和 TSDoc 文档注释要求。
2. 打开 `.github/instructions/unit-tests.instructions.md`，注意 `applyTo` frontmatter，它将说明限定在 `**/*.test.ts` 文件。

在下一部分将 `Code lacks documentation` issue 分配给云智能体时，留意生成的拉取请求中是否包含 TSDoc 文档注释、TypeScript 约定和文件注释头。这些内容来自上述说明文件。后续练习审查拉取请求（PR）时还会再次检查。

## 为云智能体设置开发环境

无论由谁编写代码，通常都需要特定环境并运行一些设置脚本，确保项目处于可用状态。将任务分配给 Copilot 也一样；它会以类似软件工程师的方式执行任务。

云智能体使用 [GitHub Actions][github-actions]准备工作环境。可以在 `.github/workflows/copilot-setup-steps.yml` 中创建[专用设置工作流][setup-workflow]，让它在开始工作前运行，以安装所需开发工具和依赖项。本实验已提前配置好该工作流，确保流程顺畅并提供实践机会。对于单个 Astro 应用，它会为 Copilot 安装 Node.js 和项目依赖项、准备端到端测试所需的浏览器二进制文件，以及迁移和填充 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 允许你从存储库的“Actions”选项卡测试这些设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 仅为这些步骤授予所需的最低权限。Copilot 会使用自己的令牌执行操作。
    permissions:
      # 如果设置步骤需要克隆存储库（例如安装依赖项），则需要 `contents: read` 权限。如果未在设置步骤中克隆，步骤完成后 Copilot 会自动为你克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置 - Node.js（整个应用现在使用 Astro + Drizzle/libSQL）
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # 迁移并填充本地 SQLite 数据库，为构建和测试准备数据。
      - name: Set up the database
        run: npm run db:setup
```

这看起来与其他 GitHub 工作流文件类似，但有几点需要注意：

- 文件中只有一个名为 `copilot-setup-steps` 的作业。Copilot 开始处理拉取请求前，GitHub Actions 会运行此作业。
- `workflow_dispatch` 触发器允许你在存储库的 **Actions** 选项卡中手动运行工作流。这有助于验证工作流，而不必等待 Copilot 启动它。

## 添加文档

多数项目都存在文档过时或缺失的问题。这类技术债务经常无人处理，会拖慢开发速度，增加代码维护难度，也让新开发者更难熟悉项目。Copilot 擅长创建文档，因此很适合把这项工作分配给 Copilot 云智能体。它会在后台生成所需文档，后续练习再审查结果。

1. 在新的浏览器选项卡中打开 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新建 issue 对话框。
4. 选择 **Blank issue**。
5. 在 **Title** 字段中输入 `Code lacks documentation`。
6. 在 **Description** 字段中输入：

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. 选择 **Create** 创建 issue。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将 issue 分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。
10. 选择 **Pull Requests** 选项卡。
11. 打开刚创建的 PR。其标题类似 `[WIP]: Code lacks documentation`。如果列表中暂时没有新 PR，请稍等片刻并刷新浏览器。
12. 几分钟后，Copilot 应会创建待办事项列表。

> [!NOTE]
> Copilot 的待办事项列表可能需要几分钟才会出现在 PR 中。Copilot 正在创建环境（运行前面介绍的工作流）、分析项目并确定合适的处理方案。

13. 查看待办事项列表和即将执行的任务。
14. 向下滚动 PR 时间线，确认 Copilot 已开始处理 issue。
15. 选择 **View session** 按钮。

   ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新页面，才能看到更新后的状态指示器。

16. 浏览实时会话，查看 Copilot 如何探索代码、了解项目状态、暂停思考并确定方案，然后创建代码。

这可能需要几分钟。Copilot 云智能体的主要优势之一是能够异步执行任务，让开发者处理其他工作。接下来利用这一点：再分配一项任务给云智能体，同时开始为应用编写其他功能。

## 在游戏详情页添加相关游戏部分

GitHub Copilot 云智能体的一项优势是可以拆分工作：你处理一组任务时，它可以处理另一组。即使为设计团队添加相关游戏部分不一定耗时，也可以把时间用于其他工作。现在将这项任务分配给云智能体。

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新建 issue 对话框。
4. 选择空白模板 **Blank issue**。
5. 在 **Title** 字段中输入 `Show related games on the game details page`。
6. 在 **Description** 字段中输入：

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. 选择 **Create** 创建 issue。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

   ![将 issue 分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

稍后，issue 中的第一条评论旁会出现一组 👀，表示 Copilot 已开始处理。

![Copilot 使用眼睛表情符号表示正在处理 issue](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在处理第二项请求。云智能体会像软件工程师一样工作，因此无需持续监控；等它完成后再审查即可。接下来开始了解和使用自定义智能体。

## 总结和后续步骤

本课介绍了 [GitHub Copilot 云智能体][copilot-agents]。可以将 issue 分配给云智能体，让它异步处理技术债务、创建新功能，或协助将代码迁移到其他框架。

本课中，你：

- 查看了 Copilot 使用的代码生成环境配置。
- 了解了安全执行操作的重要性。
- 了解了明确界定 issue 范围的重要性。
- 将 issue 分配给了 Copilot。

云智能体正在后台处理任务，现在可以开始[创建和使用自定义智能体][next-lesson]。Copilot 云智能体也[支持使用模型上下文协议（MCP）服务器][cloud-agent-mcp]，并可使用前面练习中探索过的自定义说明。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub issue 分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
