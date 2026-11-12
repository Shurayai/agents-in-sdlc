---
title: "第 7 课 - 创建并使用质量保证（QA）智能体"
description: "创建质量保证（QA）自定义智能体，结合 issue 需求、quality-checks 技能和 Playwright 模型上下文协议（MCP）。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，并通过 Playwright MCP 在浏览器中观察过滤体验。现在将这些能力整合到自定义智能体中，定义明确的 QA 流程。

在本课中，你将：

- 探索自定义智能体如何与说明、技能和 MCP 工具协作。
- 创建并检查可复用的质量保证配置。
- 选择 QA 智能体，并根据过滤功能 issue 审查其发现。

## 场景

创建拉取请求（PR）前，Tailspin Toys 希望统一检查需求、代码质量、自动化检查、测试覆盖范围和浏览器行为。自定义智能体可以协调 QA 流程并提供可复用的报告。

## 什么是自定义智能体？

自定义智能体是通过 Markdown 配置文件定义的 Copilot 专用版本。配置文件说明智能体的用途、指令和可用工具。本工作坊将在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择它。

各项自定义功能用途不同：存储库说明定义团队标准，`quality-checks` 技能封装可重复检查，Playwright MCP 提供浏览器工具，而 QA 配置则指导 Copilot 如何组合这些能力来评估需求和报告发现。QA 配置不会取代这些功能，也不需要另开对话。

## 创建 QA 配置

创建功能 PR 前，请让 Copilot 创建可复用的 QA 配置。配置中会定义 QA 执行的检查及其必须遵循的边界。

1. 返回 Codespace，并确认过滤功能对话处于交互模式。
2. 请默认智能体创建新的自定义智能体：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置

使用新智能体前，先检查配置，确认 Copilot 捕获了预期的 QA 流程和边界。这可以避免智能体在你只希望验证功能时进行不完整或过度宽泛的更改。

1. 输入 `/diff` 并打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 为必填项；`name` 为可选项，但添加后会提供清晰的显示名称。
3. 阅读配置说明，确认 QA 会从需求出发、遵循存储库说明、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持性证据，在更改实现代码前征求同意，并且不会提交更改或创建拉取请求。
5. 如果生成的配置缺少上述职责或边界，请先要求默认智能体修改，再继续。

## 根据 issue 运行 QA

Copilot CLI 会在对话启动时加载项目智能体。创建配置后，恢复同一段过滤功能对话并选择 QA，以便它使用已有的 issue 和规划决策。

1. 使用以下提示启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 刚创建的智能体可能不会立即出现在可用智能体列表中。它仍然可用，上面的命令会启用它。

2. 使用以下提示，请 QA 智能体审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. 等待 QA 智能体完成工作。
4. 阅读它提供的报告。

## 总结和后续步骤

你添加了可复用的专用角色，并审查了它的工作。在本课中，你：

- 探索了自定义智能体如何与说明、技能和 MCP 工具协作。
- 创建并检查了可复用的质量保证配置。
- 选择 QA 智能体，并根据过滤功能 issue 审查了它的发现。

现在，实现、技能更新、QA 配置、测试和验证报告均已准备好接受审查。接下来，[将它们汇总到功能 PR 中并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
