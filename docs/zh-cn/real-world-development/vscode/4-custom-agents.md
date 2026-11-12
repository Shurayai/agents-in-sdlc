---
title: "练习 4 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

GitHub Copilot 中的[自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的人工智能（AI）助手。将智能体定义为存储库 `.github/agents` 文件夹中的 Markdown 文件后，可以为 Copilot 提供专门的说明、最佳实践、编码模式和领域知识，帮助它更有效地完成特定类型的工作。团队可以把专业经验整理为可复用的智能体，例如执行[网站内容无障碍指南（WCAG）][wcag]的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体可以通过项目 `.github/agents` 文件夹中的 Markdown 文件定义，也可以在全局路径 `~/.copilot/agents` 中定义。每个文件都包含 YAML（YAML Ain't Markup Language）frontmatter，至少包含 `name` 和 `description`，后续 Markdown 提示用于定义智能体的行为、专业知识和指令。

### 自定义智能体与智能体技能的区别

自定义智能体和[智能体技能][agent-skills-concept]有些相似：两者主要通过 Markdown 文件定义，都会告诉 AI 如何执行任务。可以这样区分：**自定义智能体负责工作，技能是它使用的工具**。

自定义智能体有自己的上下文窗口，并且可以协调技能，甚至其他智能体来完成工作。在本实验中，无障碍自定义智能体会根据无障碍指南审查并更新网站；它还可以调用拉取请求工作流技能，或运行和管理测试的技能。

> [!NOTE]
> 自定义智能体没有唯一的正确写法。与 AI 的其他用法一样，需要在自己的环境和场景中测试并迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## 场景

Tailspin Toys 致力于让所有用户都能使用其众筹平台，不受视觉能力或偏好影响。近期用户反馈指出，部分用户认为当前深色主题难以阅读，因为文本和背景颜色的对比度不足。为解决这一无障碍问题，设计团队要求实现可由用户开启或关闭的高对比度模式。

无障碍访问至关重要，因此希望尽快实现这一功能。接下来将使用自定义智能体生成相关功能。

在本练习中，你将：

- 查看现有的无障碍自定义智能体。
- 在 Copilot Chat 中使用无障碍智能体实现高对比度模式。

## 检查无障碍自定义智能体

项目已经包含一个无障碍自定义智能体。先查看其内容，了解它将如何指导 Copilot。

返回 Codespace 并准备一个分支，用于开展无障碍功能工作，将其与练习 3 中的过滤功能拉取请求（PR）分开。

1. 在终端中从 `main` 创建并切换到新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. 打开 `.github/agents/accessibility.md`。
3. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

4. 接着浏览后续部分，了解其中介绍的内容：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - 超文本标记语言（HTML）、层叠样式表（CSS）和 JavaScript 代码示例。
   - 常见陷阱和错误。

## 在 Copilot Chat 中使用自定义智能体

VS Code 会在 Copilot Chat 视图底部的智能体下拉列表中显示 `.github/agents` 中定义的所有自定义智能体。选择自定义智能体后，该 Chat 会话就会遵循相应指令和工具配置。

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始全新对话。模式和模型的选择因练习而异；相关步骤会在需要时说明。

1. 如果 Chat 视图的智能体下拉列表中尚未选中 **Agent**，请先选择它。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 选择 Chat 视图底部的智能体下拉列表（其中显示当前智能体，默认是 **default**）。
3. 从可用智能体列表中选择 **Accessibility agent**。
4. 向无障碍智能体发送以下提示：

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat 会开始工作：探索代码库、提出更改并修改项目文件。每项编辑都会在 Chat 中显示文件路径和差异，供你审查。
6. 随着编辑发生，**Files changed** 指示器会更新，显示智能体修改的文件。

> [!NOTE]
> 这可能需要几分钟。Copilot 会实际修改存储库，可能会更新 Astro 组件、CSS 和相关测试等现有文件。

下一练习会审查并引导这项正在进行的工作。

## 总结和后续步骤

本课中，你：

- 查看了现有的无障碍自定义智能体。
- 在 Copilot Chat 中使用无障碍智能体实现了高对比度模式。

接下来，[监控并引导智能体的工作][next-lesson]，在更改进行时审查它们，并在同一个会话中添加浅色模式切换。

## 资源

- [关于自定义智能体][custom-agents]
- [在集成开发环境（IDE）中创建自定义智能体][creating-custom-agents-ide]
- [VS Code 中的自定义智能体][custom-agents-vscode]
- [自定义智能体配置][custom-agents-config]
- [awesome-copilot 上的自定义智能体][awesome-copilot-agents]

---

| [← 上一课：使用 Playwright 模型上下文协议（MCP）服务器测试功能][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
