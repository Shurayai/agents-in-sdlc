---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在本实验中，你与 GitHub Copilot 一起完成了多项改进用户体验和添加功能的任务：为代码添加文档、构建相关游戏功能供设计团队迭代，以及实现包括高对比度和浅色模式切换在内的无障碍功能。现在检查代码更改；必要时向 Copilot 提供反馈，进一步改进结果。

### 场景

正如前面多次强调的那样，引入生成式人工智能（AI）并不会改变软件设计和开发运维（DevOps）的基本原则。始终需要审查生成的代码，并遵循正常的 DevOps 流程。现在先审查 GitHub Copilot 为文档、相关游戏功能和无障碍功能提出的更改，然后再允许团队其他成员审查。

## 安全性和 GitHub Copilot 云智能体

Copilot 云智能体会在无人监督的情况下异步执行任务，因此采取了安全限制：

- Copilot 只能读取存储库，并且**只能**写入用于处理代码的分支。
- 云智能体在 GitHub Actions 中运行，并在单独的临时环境中工作。
- 运行任何 GitHub Actions 工作流前，都需要人工审批。
- 默认情况下，[对外部资源的访问受限](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，模型上下文协议（MCP）服务器也包括在内。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求（PR），其中包含为代码添加的文档。通过 GitHub.com 标准 PR 界面完成审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限地访问外部资源，包括外部 MCP 服务器。你也可以[自定义或禁用 Copilot 云智能体的防火墙][agent-firewall]。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests**，打开 PR 列表。
3. 打开标题类似 **Add missing documentation** 或更完整描述的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。此时请等待 Copilot 完成任务。这可能需要几分钟，可以休息片刻或回顾已学内容。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

   ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看更新后的代码，其中应包含新创建的 TSDoc 文档注释和其他文档。具体更改会有所不同。

   审查时，查找 TSDoc 文档注释、TypeScript 约定和文件注释头。这些来自练习 2 开始时查看的自定义说明文件。

6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流正在等待审批的指示。
8. 如果有工作流等待审批，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应在 PR 的检查区域中排队运行。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。

## 请求 GitHub Copilot 修改

与 Copilot 协作并非单向过程。你可以像在团队协作中一样，在 PR 评论或代码行内评论中提及 Copilot。Copilot 会读取评论，并启动新的会话来处理请求。由于结果具有非确定性，无法规定必须提出的具体请求。可以要求 Copilot：

- 在每个代码文件顶部添加简要说明文件用途的注释头。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用结构。

1. 添加评论，请 Copilot 修改生成的文档，并像提及其他用户一样标记 **@copilot**。可以使用上面的建议，也可以提出其他文档改进请求。
2. 选择 **View Session**，查看 Copilot 如何处理任务。注意它会启动新会话来完成更新。
3. 选择 **Back to pull request**，返回 PR。

   ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，PR 中应出现新的提交。
5. 选择 **Files changed** 选项卡并审查更改。

6. 如有需要，继续迭代，直到满意为止。
7. 确认无误后，将 PR 从草稿状态改为准备审查，然后合并到 `main` 分支。

![将 PR 转为准备审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

返回 Copilot 为“在游戏详情页显示相关游戏”issue 创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 或更完整描述的 PR。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有工作流正在等待审批的指示。
7. 如果有工作流等待审批，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. 工作流应在 PR 的检查区域中排队运行。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。
9. **可选：**也可以在 Codespace 中检出此分支，手动测试相关游戏功能。打开 Codespace 和终端，运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名，例如 **copilot/fix-8**）：

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

Copilot 已构建相关游戏功能。与之前一样，可以通过评论继续迭代并请求云智能体更新。

10. 如需迭代，请在 **Conversation** 选项卡中添加评论，说明更新请求。例如，可以调整显示的相关游戏数量，或要求添加文件注释头和 TSDoc 文档注释。请记住，分配此任务时尚未更新自定义说明。

## 审查无障碍功能

最后，审查使用无障碍自定义智能体实现的功能。此 PR 应同时包含练习 3 中分配的高对比度模式，以及练习 4 在任务控制中心中提出的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 或更完整描述的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会带有 **[WIP]** 标记。此时请等待 Copilot 完成任务，可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 检查实现，尤其关注以下方面：
   1. 用于切换模式的用户界面（UI）组件。
   2. 用于保存用户偏好的本地存储。
   3. 高对比度模式和浅色模式的层叠样式表（CSS）或样式更改。
   4. 无障碍富互联网应用（ARIA）属性、键盘导航等。
   5. 管理模式切换的 JavaScript/TypeScript 代码。
6. 审查更新并确认符合预期后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流正在等待审批的指示。
8. 如果有工作流等待审批，请选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应在 PR 的检查区域中排队运行。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。
10. **可选：**可以在 Codespace 中检出此分支，手动测试无障碍功能。打开 Codespace 和终端，运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式切换，确认它们正常工作，并且在重新加载页面后仍会保留设置。

无障碍自定义智能体帮助 Copilot 根据无障碍最佳实践实现这些功能。

11. 如果发现无障碍问题或改进点，请像处理之前的 PR 一样，在评论中标记 **@copilot** 请求更新。

## 可选练习——继续委派任务

云智能体最适合处理真实待办事项，让你能同时专注于其他工作。可以在自己的存储库中创建更多 issue 并分配给 Copilot，以培养这种工作习惯。以下是一些想法：

- 在游戏详情页创建支持者意向表单。
- 为游戏列表页实现分页。
- 为数据访问 helper 添加输入验证和错误处理。

## 总结

你已完成云智能体工作坊。在这些课程中，你：

- **检查了存储库附带的自定义说明文件**，以便之后观察它们对云智能体输出的影响。
- **将 issue 分配给 Copilot 云智能体**，并观察它设置环境、制定计划和异步执行任务。
- **创建并使用无障碍自定义智能体**，添加高对比度和浅色模式切换。
- **将 Copilot 智能体页面用作任务控制中心**，监控并引导正在进行的无障碍会话。
- **审查并迭代云智能体创建的拉取请求**，标记 `@copilot` 请求更改并审批工作流。

## 回顾和后续步骤

云智能体工作坊已完成。其他工作坊可以帮助你继续探索：

- 🖥️ **[VS Code 工作坊](../../vscode/)**——在集成开发环境（IDE）中探索 Copilot Chat 智能体模式和 MCP 集成。
- 💻 **[CLI 工作坊](../../cli/)**——从终端交付两项经过审查的更改，体验计划和自动驾驶模式、智能体技能、自定义质量保证（QA）智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

还可以在自己的存储库中尝试以下后续任务：

- 将重构或测试覆盖率 issue 分配给云智能体。
- 为其他领域创建自定义智能体。
- 为其他技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub issue 分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
