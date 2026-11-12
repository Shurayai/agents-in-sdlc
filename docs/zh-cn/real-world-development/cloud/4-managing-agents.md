---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前几项练习中，你让 Copilot 云智能体处理了三项改进用户体验和添加功能的任务。尽管云智能体会异步自主工作，监控这些任务仍然很重要。

可以通过多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，可以查看所有有未关闭拉取请求（PR）的智能体任务，了解已执行的操作，还可以引导正在进行的会话。

在本练习中，你将：

- 浏览智能体页面，监控云智能体任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

将高对比度模式任务分配给智能体后，团队决定顺便添加浅色模式。由于智能体已经在更新网站样式并添加切换功能，因此一并实现浅色模式很合理。现在引导智能体同时添加浅色模式和高对比度模式。

## 查看 Copilot 云智能体任务

查看分配给 Copilot 云智能体的所有任务的当前状态。

1. 打开 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主区域和左侧区域中的任务列表。应能看到分配给 Copilot 的任务，包括：
   - 更新代码文档。
   - 生成用于修改游戏的应用程序编程接口（API）。
   - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作，例如：
   - 从存储库检出代码。
   - 为 Copilot 创建环境。
   - 设置模型上下文协议（MCP）服务器。
   - 执行完成分配任务所需的其他步骤。

> [!NOTE]
> 具体步骤会根据 Copilot 的工作状态和采用的方案而有所不同。

4. 查看右侧显示的拉取请求（PR）区域，其中可以查看 PR 和已更改的文件，以便进一步监控。

## 引导云智能体

你已查看当前正在执行的任务。现在请 Copilot 在实现高对比度模式时，也添加浅色模式切换开关。

1. 选择与添加高对比度模式相关的会话。具体标题会因 Copilot 使用的名称和当前工作状态而异。

   ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到设置完成并开始执行任务。此时会出现类似下文的消息。
3. 在 **Steer active session while Copilot is working** 对话框中，输入以下提示：

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![智能体页面中的云智能体任务，突出显示“Steer active session while Copilot is working”对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 查看 Copilot 如何确认提示，并将其纳入任务流程。

## 让 Copilot 继续工作

与之前一样，Copilot 会继续处理更新后的任务。完成发送提示时正在执行的步骤后，它会将新请求加入工作流程。

这同样需要几分钟，可以趁此回顾目前学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot 智能体页面——监控和引导 GitHub Copilot 云智能体任务的中心位置。你可以通过该任务控制中心跟踪所有正在进行和已完成的任务、审查工作过程，并调整正在进行任务的范围或补充指导。

本课中，你：

- 使用任务控制中心和智能体页面监控了云智能体任务。
- 引导了正在进行的会话，请求添加其他功能。

Copilot 正在完成无障碍功能，接下来可以[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
