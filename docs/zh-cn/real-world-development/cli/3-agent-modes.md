---
title: "第 3 课 - 智能体模式：计划和自动驾驶"
description: "使用计划模式确定方案、自动驾驶模式根据 issue 构建过滤功能，并通过交互模式审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们已经为项目添加了一项小功能，但更大的更改需要更完善的流程。GitHub Copilot CLI 可以配合组织现有的工作流，帮助按正确方式构建正确的内容。本课将开始一系列遵循典型智能体驱动开发流程的课程：从 issue 开始构建新功能，确保代码有效、功能符合预期，最终成功合并到项目中。

> [!NOTE]
> 后续功能开发将继续使用同一段对话和同一个分支。实际工作中，不同文件类型的更改通常会使用不同分支或拉取请求（PR）；此处为聚焦核心概念而简化流程。

在本课中，你将：

- 从 GitHub issue 启动新的 Copilot 对话。
- 在计划模式中明确需求。
- 使用自动驾驶模式实现新功能。
- 审查代码。
- 在转发的浏览器中手动验证功能。

继续开发该功能时，你还将更新存储库说明、自定义现有的 `quality-checks` 技能、添加 MCP 验证、创建 QA 智能体并创建功能 PR。

## 场景

Tailspin Toys 的目录不断扩大，访问者需要按类别和发布商筛选游戏。待办事项中的 issue 描述了这项功能，但在开始编码前，仍需确定如何组合多个类别等细节。你将使用计划模式确定这些决策，然后授权自动驾驶模式在明确范围内实现功能。

## 背景

将人工智能（AI）编码智能体引入开发流程，并不会改变基本原则。事实上，这些原则变得更加重要。多数开发者遵循的流程大致如下：

1. 从描述需求的 issue 开始。
2. 制定构建方案。
3. 编写并审查代码。
4. 运行测试验证代码。
5. 手动验证新功能。
6. 创建拉取请求（PR）。
7. 代码经过审查且持续集成流程成功后，合并代码。

> [!NOTE]
> 具体流程因团队和组织而异，但大多数流程都与上述做法相近。

遵循这种标准方法，可以确保 AI 生成的代码符合要求，并经过与手写代码相同的验证流程。

## 对话模式

**对话模式**决定智能体可以自主执行工作的程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与智能体协作。智能体提出更改建议，并等待你的输入后再继续。
- **Plan**：智能体先制定计划，但不能编辑项目文件。
- **Autopilot**：智能体自主编写代码、运行测试并迭代，直到认为任务完成。

先使用计划模式审查方案，然后使用自动驾驶模式实现方案。

## 从 issue 开始

开始过滤功能前，返回 Codespace，确认存储库和终端已准备就绪。

1. 返回 Codespace。如果它已停止，请先重启。
2. 确认星级评分 PR 已合并。
3. 如果终端尚未打开，按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
4. 更新 `main`，然后为过滤功能创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 按两次 <kbd>Tab</kbd> 打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有 issue。
8. 使用方向键选中标题为 **Allow users to filter games by category and publisher** 的 issue。
9. 按 <kbd>C</kbd> 将 issue 添加到提示中，并返回 **Session** 选项卡。

现在提示中应出现 `#7`（或类似编号）。在提示中加入 `#`，即可引用 GitHub 上的 issue 或拉取请求（PR）。

## 规划过滤功能

制定计划有助于在交给 Copilot 执行前明确功能实现方式。对于复杂任务，花些时间规划通常很有帮助。现在切换到计划模式，请 Copilot 制定计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到计划模式。确认提示下方的模式指示器显示 **Plan**。
2. 在上一步添加的 issue 引用后输入以下提示：

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot 会开始探索项目并确定合适的实现方案，进而制定计划。

3. Copilot 可能会询问过滤功能应如何工作。根据预期回答即可。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 上下滚动审查计划。
6. 如果计划中的任何内容不符合你的决定，请要求 Copilot 修改。

## 批准自动驾驶模式

计划制定并审查完毕后，就可以开始实现。自动驾驶模式允许 Copilot 持续迭代，直到它认为任务完成。

1. 选择 **Accept plan and build on autopilot (recommended)**，或所安装版本中含义相同的选项。
2. 确认提示下方的模式指示器显示 **Autopilot**。
3. 观察 Copilot 如何根据计划迭代、生成代码并运行测试。

> [!NOTE]
> 批准后可能会立即开始实现，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决设置问题，再判断检查是否完成。

## 审查并验证实现

与其他代码一样，生成的代码在合并前也需要审查。检查代码并运行网站，确认功能正常。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 进入交互模式。确认模式指示器不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`，检查过滤功能实现和测试。
3. 对照 issue 和规划时确定的行为审查结果。
4. 审查代码后，按 <kbd>Esc</kbd> 退出差异视图。
5. 查看项目检查结果；如有失败，请 Copilot 修复。

## 体验新功能

代码看起来没问题，但还需要确认它能运行。像之前一样启动应用，并通过 Codespaces 转发的端口打开网站。

1. 请 Copilot 启动应用：

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. 当 Codespaces 提示端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别筛选、按发布商筛选，以及按计划确定的组合方式筛选。
4. 确认重置和无结果时的行为符合 issue 和你的决定。
5. 返回 Codespace，并请 Copilot 停止它启动的开发服务器。

## 总结和后续步骤

你已使用不同的对话模式构建并审查功能。在本课中，你：

- 从 GitHub issue 启动了新的 Copilot 对话。
- 在计划模式中明确了需求。
- 使用自动驾驶模式实现了功能。
- 审查了代码。
- 在转发的浏览器中手动验证了功能。

接下来，使用[自定义说明][next-lesson]深入了解如何让代码遵循已记录的实践。

## 资源

- [GitHub Copilot CLI 中的自动驾驶模式][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
