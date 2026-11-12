---
slug: zh-cn/real-world-development/cloud
title: "GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent)** 可在云端异步处理工作。你在 GitHub 上分配任务后，云智能体会在后台探索存储库、进行更改并创建拉取请求，你则可以继续处理其他工作。

本工作坊将先添加云智能体会遵循的自定义说明，再分配 GitHub issue 并让它实现任务。你将审查并使用自定义智能体来指导其工作方式，在智能体仪表板中监控和引导会话，最后审查它创建的拉取请求并迭代改进结果。

## 练习

| 练习 | 主题 | 说明 |
| ---- | ---- | ---- |
| [0. 先决条件][ex0] | 设置 | 创建存储库和 Codespace |
| [1. 自定义说明][ex1] | 上下文 | 添加云智能体将遵循的自定义说明 |
| [2. 云智能体][ex2] | 异步智能体 | 将 issue 分配给 Copilot 云智能体 |
| [3. 自定义智能体][ex3] | 专用智能体 | 审查并使用自定义智能体 |
| [4. 管理智能体][ex4] | 监控 | 监控和引导智能体会话 |
| [5. 迭代][ex5] | 审查 | 审查拉取请求（PR）、迭代 Copilot 的工作并选择后续步骤 |

## 先决条件

参加本工作坊前，请确保具备以下条件：

- [ ] 拥有有效的 **Copilot Student、Pro、Pro+、Business 或 Enterprise** 计划的 GitHub 账户
- [ ] 已为账户或组织启用 Copilot 云智能体

> [!TIP]
> 没有付费计划？经验证的学生可以通过 [GitHub Education][student-plan] 免费使用 GitHub Copilot。**Copilot Student** 计划包含本工作坊使用的智能体、模型上下文协议（MCP）、代码审查和 Copilot CLI 功能。

[student-plan]: https://github.com/education/students

> [!NOTE]
> 除 Copilot Free 外，Copilot Student、Pro、Pro+、Business 和 Enterprise 均可使用云智能体。对于 Copilot Business 或 Enterprise，管理员必须为组织启用此功能。

> [!NOTE]
> 本工作坊不涉及 MCP。若要了解如何将 MCP 服务器与 Copilot 配合使用，请参阅 [CLI 工作坊][cli]或 [VS Code 工作坊][vscode]。

## 开始

**[从练习 0：先决条件开始 →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
[cli]: ../cli/
[vscode]: ../vscode/
