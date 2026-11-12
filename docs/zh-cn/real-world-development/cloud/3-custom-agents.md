---
title: "练习 3 - 自定义智能体"
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

本练习将介绍自定义智能体：

- 如何定义自定义智能体。
- 如何向自定义智能体分配任务。

## 场景

Tailspin Toys 致力于让所有用户都能使用其众筹平台，不受视觉能力或偏好影响。近期用户反馈指出，部分用户认为当前深色主题难以阅读，因为文本和背景颜色的对比度不足。为解决这一无障碍问题，设计团队要求实现可由用户开启或关闭的高对比度模式。

无障碍访问至关重要，因此希望尽快实现这一功能。接下来将使用自定义智能体生成相关功能。

## 检查无障碍自定义智能体

项目已经包含一个无障碍自定义智能体。先查看其内容，了解它将如何指导 Copilot。

返回 Codespace，然后检查无障碍自定义智能体文件：

1. 打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

3. 接着浏览后续部分，了解其中介绍的内容：
   - 为无障碍网站生成代码时的核心职责。
   - 无障碍最佳实践。
   - 超文本标记语言（HTML）、层叠样式表（CSS）和 JavaScript 代码示例。
   - 常见陷阱和错误。

## 创建并分配 issue

任务控制中心是管理环境中所有智能体的中心位置。可以在其中向 Copilot 云智能体分配任务、监控任务，以及调整任务方向或提供更多指导。现在将创建高对比度模式的任务并分配给 Copilot。

1. 打开存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新建 issue 对话框。
4. 选择 **Blank issue**。
5. 在 **Title** 字段中输入 `Add high contrast mode to website`。
6. 在 **Description** 字段中输入：

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

7. 选择 **Create** 创建 issue。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。
9. 从自定义智能体列表中选择 **Accessibility agent**。

   ![Copilot 云智能体分配界面，突出显示自定义智能体选择器和 Accessibility agent](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot 将在后台开始处理任务。

## 总结和后续步骤

本课介绍了 GitHub Copilot 中针对特定任务和领域定制的[自定义智能体][custom-agents]。可以使用自定义智能体将团队的专业知识和标准整理为可复用的配置，指导 Copilot 更有效地完成特定类型的工作。

本课中，你：

- 了解了如何定义自定义智能体。
- 向自定义智能体分配了任务。

Copilot 正在实现高对比度模式，接下来可以在任务控制中心[监控并引导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [在组织中准备使用自定义智能体][org-custom-agents]
- [在企业中准备使用自定义智能体][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot 云智能体][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
