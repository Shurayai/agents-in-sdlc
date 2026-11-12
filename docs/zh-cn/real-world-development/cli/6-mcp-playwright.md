---
title: "第 6 课 - 使用 Playwright 模型上下文协议（MCP）验证功能"
description: "在 Copilot CLI 中检查或配置 Playwright MCP，并使用它在浏览器中体验过滤功能。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

编写代码只是开发工作的一部分。还需要处理数据、外部服务，并让 Copilot 使用更多自动化工具。模型上下文协议（MCP）服务器可以扩展 Copilot CLI 的内置能力，为其提供其他工具和服务。

在本课中，你将：

- 了解模型上下文协议（MCP）及 Copilot CLI 如何使用它。
- 如果尚未配置 Playwright MCP 服务器，则添加它。
- 请智能体驱动浏览器，体验过滤功能。

## 场景

单元测试和端到端测试很重要，但验证用户界面（UI）更新还需要实际与界面交互。让 Copilot 像用户一样操作正在开发的网站，可以进一步自动化更改验证，并增强对功能行为的信心。

## 什么是模型上下文协议（MCP）？

[模型上下文协议（MCP）][mcp-blog-post]让人工智能（AI）智能体能够与外部工具和服务通信。使用 MCP 后，智能体可以实时访问最新信息，并代表你执行操作。

MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁。每个 MCP 服务器都代表一组智能体可以访问的工具和资源。常见的 MCP 服务器包括：

- **[GitHub MCP Server][github-mcp]**：提供用于管理 GitHub 存储库、issue 和拉取请求的应用程序编程接口（API）。
- **[Playwright MCP Server][playwright-mcp-server]**：使用 Playwright 提供浏览器自动化能力。

还有许多其他 MCP 服务器。GitHub 提供了 [MCP 注册表][mcp-registry]，帮助开发者发现并为生态系统做出贡献。

> [!CAUTION]
> 对待 MCP 服务器应像对待项目中的其他依赖项一样。使用前请审查其源代码、验证发布者并考虑安全影响。

## 添加 Playwright MCP 服务器

如果尚未配置 Playwright MCP 服务器，请添加它，以便 Copilot 像用户一样操作网站。

> [!NOTE]
> 如果 Copilot CLI 中已配置 Playwright MCP，请跳过以下设置步骤，继续下一部分。

1. 返回 Codespace。
2. 在 Copilot CLI 中输入以下命令，打开添加 MCP 服务器的对话框：

   ```plaintext
   /mcp add
   ```

3. 输入名称 `playwright`，然后按 <kbd>Tab</kbd>。
4. 按 <kbd>Enter</kbd> 确认服务器类型为 **STDIO**，然后按 <kbd>Tab</kbd>。
5. 在 **Command** 对话框中粘贴以下命令：

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. 按 <kbd>Control</kbd>+<kbd>S</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>S</kbd>（Windows/Linux）保存新的 MCP 服务器。
7. 按 <kbd>Esc</kbd> 退出 MCP 对话框。

## 请 Copilot 使用 Playwright 体验功能

此前你已手动确认功能行为符合预期。现在使用 Copilot 中的 Playwright MCP 服务器完成同样的检查。

1. 使用以下提示，请 Copilot 通过 Playwright MCP 验证功能：

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> 通常无需明确指定 MCP 服务器，Copilot 会自行判断是否使用。但明确指出所需工具有助于保持一致并减少不必要的交互。

2. 观察 Copilot 如何列出它在浏览器中执行的操作，以确认功能是否正常。
3. 阅读报告，确认所有行为符合预期。

Copilot 会启动服务器，使用 Playwright 操作网站，停止服务器，然后提供报告。

## 总结和后续步骤

你已使用 Playwright MCP 服务器，让 Copilot CLI 在真实浏览器中体验功能。具体来说，你：

- 了解了模型上下文协议（MCP）以及 Copilot CLI 如何使用它。
- 如果此前未配置 Playwright MCP 服务器，则添加了该服务器。
- 请智能体驱动浏览器并体验过滤功能。

接下来，[创建 QA 自定义智能体][next-lesson]，将技能和浏览器工具整合到专用角色中。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [向 Copilot CLI 添加 MCP 服务器][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
