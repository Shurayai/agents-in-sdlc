---
title: "练习 3 - 使用 Playwright 模型上下文协议（MCP）服务器测试功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：智能体模式][previous-lesson] · [下一课：自定义智能体 →][next-lesson]

你刚使用智能体模式构建了过滤功能。创建拉取请求前，应确认它在浏览器中正常工作。无需亲自逐项操作应用；可以连接 **Playwright MCP 服务器**，让 Copilot 驱动真实浏览器测试功能，然后发布分支并创建 PR。

在本练习中，你将：

- 了解模型上下文协议（MCP）以及 MCP 服务器如何为 Copilot 扩展工具。
- 将 Playwright MCP 服务器添加到工作区。
- 请 Copilot 使用它在浏览器中手动测试过滤功能。
- 发布分支，并为过滤功能创建拉取请求。

## 什么是模型上下文协议（MCP）？

智能体模式能够访问编辑器以外的工具后，功能会大幅增强。模型上下文协议（MCP）是 Copilot 用来实现这一点的标准，可让智能体与外部工具和服务通信。

![智能体模式与上下文、大语言模型和工具的交互示意图，其中包括由 MCP 服务器和 VS Code 扩展提供的工具](../../../_images/ex1-mcp-diagram.png)

[模型上下文协议（MCP）](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/)让人工智能（AI）智能体能够与外部工具和服务通信。使用 MCP 后，AI 智能体可以实时访问最新信息（通过资源）并代表你执行操作（通过工具）。

AI 智能体通过 MCP 服务器访问这些工具和资源。MCP 服务器充当 AI 智能体与外部工具和服务之间的桥梁，负责管理智能体与外部工具（例如已有 API 或 npm 包等本地工具）之间的通信。每个 MCP 服务器代表一组智能体可以访问的工具和资源。

常见的 MCP 服务器包括：

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**：提供一组用于管理 GitHub 存储库的应用程序编程接口（API），让 AI 智能体可以创建存储库、更新已有存储库、管理 issue 和拉取请求等。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**：使用 Playwright 提供浏览器自动化能力，让 AI 智能体可以访问网页、填写表单和选择按钮等。

还有许多其他 MCP 服务器可以提供不同的工具和资源。GitHub 提供了 [MCP 注册表](https://github.com/mcp)，帮助开发者发现服务器并为生态系统做出贡献。

> [!CAUTION]
> 从安全角度看，应像对待项目中的其他依赖项一样对待 MCP 服务器。使用前请仔细审查源代码、验证发布者并考虑安全影响。只使用信任的 MCP 服务器，并谨慎授予其访问敏感资源或执行操作的权限。

## 查看 MCP 配置

`.vscode/mcp.json` 文件用于配置 VS Code 工作区可使用的 MCP 服务器。

1. 在 Codespace 中打开 `.vscode/mcp.json`。
2. 查看已配置的 `github` 服务器：

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

项目模板已包含此 `github` 条目，因此 Copilot 能在前一练习中读取待办事项中的 issue。它使用[远程 GitHub MCP 服务器][remote-github-mcp-server]，无需本地安装；VS Code 通过超文本传输协议（HTTP）连接，并在 Copilot 首次使用其工具时要求你通过 GitHub 身份验证。

## 添加 Playwright MCP 服务器

现在添加第二个服务器。[Playwright MCP 服务器][playwright-mcp-server]为 Copilot 提供可控的浏览器，正好可用于测试功能。

1. 在 `.vscode/mcp.json` 中，在 `github` 旁添加 `playwright` 条目，使文件内容如下：

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. 保存文件。

与远程 `github` 服务器不同，`playwright` 是**本地**服务器：VS Code 会运行 `npx @playwright/mcp@latest` 启动它。`--headless` 标记让 Playwright 在后台运行浏览器，不显示窗口。Codespace 中没有桌面环境，因此必须使用此设置。

> [!NOTE]
> Tailspin Toys 项目已在端到端测试中使用 Playwright，通常已安装 Playwright 所需的浏览器。如果 Copilot 后续报告缺少浏览器，请让它运行 `npx playwright install chromium`，然后重试。

## 启动并信任服务器

VS Code 会**按需**启动 MCP 服务器：Copilot 首次需要服务器工具时，VS Code 会启动服务器并询问你是否信任它。

1. 在 `.vscode/mcp.json` 中，`playwright` 条目上方会出现 **Start** 操作。选择它立即启动服务器，确认配置正确。
2. 如果 VS Code 询问是否信任服务器，请审查配置并选择信任，以便启动服务器。

手动启动是可选的。如果跳过，VS Code 会在下一步 Copilot 首次需要服务器工具时启动服务器，并询问是否信任。

## 测试过滤功能

[Playwright MCP 服务器][playwright-mcp-server]为 Copilot 提供真实浏览器。它可以打开页面、导航、应用筛选条件并读取结果，然后总结观察到的内容。无需离开对话即可快速确认功能是否符合预期。

Playwright MCP 服务器基于页面的[无障碍树][playwright-mcp-server]而不是屏幕截图工作。智能体会像辅助技术一样，根据结构化且带标签的元素（按钮、链接和列表项）进行判断，因此简单的功能检查也能兼顾基本的无障碍验证。

服务器已连接且应用正在运行后，请 Copilot 使用浏览器测试刚构建的过滤功能。

1. 发送以下提示：

   ```text
   Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

   1. Go to the games page and note how many games are listed.
   2. Apply a category filter and confirm the list updates to only show games in that category.
   3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
   4. Combine a category and a publisher filter and confirm the results respect both.

   Report what you observe at each step, and call out anything that does not behave as expected.
   ```

Copilot 会通过 Playwright MCP 服务器启动浏览器，执行每一步并报告结果。对照 issue 中的验收标准审查报告；如果发现异常，请追问或让 Copilot 修复代码，然后再创建拉取请求。

> [!NOTE]
> 测试时，应用必须在 `http://localhost:4321` 运行。如果已停止开发服务器，请在发送提示前重新启动。Copilot 首次使用 Playwright MCP 服务器时，可能需要下载浏览器；如果报告缺少浏览器，请让它运行 `npx playwright install chromium` 并重试。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## 发布分支并创建拉取请求

确认功能正常后，就可以发布 `filtering-vscode` 分支并创建拉取请求，供团队审查。

1. 在 Codespace 中打开 **Source Control** 面板，审查 Copilot 所做的更改。
2. 选择 **+** 暂存更改。
3. 使用 **Sparkle** 按钮生成提交消息。

   ![显示 Copilot 所做更改的 Source Control 面板](../../../_images/ex3-source-control-changes.png)

4. 选择 **Publish**，将分支推送到存储库。

## 创建拉取请求

可以通过多种方式创建拉取请求，例如在 github.com 上操作，或使用 GitHub 命令行界面（CLI）。现在仍在使用 GitHub Copilot，因此可以让它创建 PR。它可以查找相关 issue，并将 PR 与其关联。

1. 打开 Copilot Chat 面板并选择 **New Chat**，启动新会话。
2. 确认智能体下拉列表中选中 **Agent**，以便 Copilot 使用 GitHub 工具。
3. 使用以下提示，请 Copilot 创建 PR：

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 根据需要选择 **Continue**，允许 Copilot 收集信息并执行操作。首次使用 GitHub 工具时，系统可能会要求你通过 GitHub 身份验证；按提示授权即可。
5. 查看 Copilot 如何搜索 issue、找到正确项并创建 PR。
6. 选择 Copilot 生成的链接，审查拉取请求，但**暂时不要合并**。

## 总结和后续步骤

本练习中，你：

- 了解了模型上下文协议（MCP）以及 MCP 服务器如何为 Copilot 扩展工具。
- 将 Playwright MCP 服务器添加到了工作区。
- 使用它在发布功能前通过浏览器手动测试了过滤功能。
- 发布了分支，并为过滤功能创建了拉取请求。

你使用 MCP 服务器测试了功能，但 MCP 只是扩展 Copilot 的一种方式。接下来，[创建自定义智能体][next-lesson]，以便处理无障碍审查等特定任务。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP 注册表][mcp-registry]
- [VS Code 中的 MCP 服务器][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
