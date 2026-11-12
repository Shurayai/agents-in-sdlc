---
title: "练习 0：先决条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

开始 VS Code 练习前，请先做好准备。你将创建一份 Tailspin Toys 存储库副本，启动用于开发的 [Codespace][codespaces]，并确认编辑器中的 GitHub Copilot Chat 已启动。

## 设置实验存储库

你将从[模板存储库][template-repository]创建自己的存储库副本。新存储库包含实验所需的全部文件，后续练习会在其中进行。

1. 在新的浏览器窗口中打开 [Tailspin Toys 模板][tailspin-template]。
2. 在实验存储库页面中选择 **Use this template**，然后选择 **Create a new repository**。

   ![“Use this template”按钮](../../../_images/ex0-use-template.png)

3. 如果你参加由 GitHub 或 Microsoft 举办的活动，请遵循导师提供的说明。否则，可以在你有权使用 GitHub Copilot 的组织中创建新存储库。

   ![模板存储库设置的输入界面](../../../_images/ex0-repository-settings.png)

4. 记下新建存储库的路径（**组织或用户名/存储库名称**），后续练习会用到。

> [!NOTE]
> **待办事项已准备就绪**
>
> 从模板创建存储库时，系统会自动为你创建一组 GitHub issue。整个工作坊都会处理这些 issue，无需自行创建。

## 创建 Codespace

接下来，使用 Codespace 完成本实验。

[GitHub Codespaces][codespaces] 是一种基于云的开发环境，可让你直接在浏览器中编写、运行和调试代码。它提供功能齐全的集成开发环境（IDE），支持多种编程语言、扩展和工具。

1. 打开刚创建的存储库。
2. 选择绿色的 **Code** 按钮。

   ![选择 Code 按钮](../../../_images/ex0-code-button.png)

3. 选择 **Codespaces** 选项卡，然后选择 **+** 按钮创建新的 Codespace。

   ![创建新的 Codespace](../../../_images/ex0-create-codespace.png)

创建 Codespace 需要几分钟，但仍比手动安装所有服务快得多。等待期间，可以先探索 GitHub Copilot 的其他功能，接下来就会开始使用它们。

> [!CAUTION]
> 后续练习还会用到此 Codespace。现在先不要关闭它，请在浏览器选项卡中保持打开状态。

> [!NOTE]
> 本工作坊可在 Codespace 或本地[开发容器][dev-containers]中运行。两者都会准备好所需的环境和依赖项。如果想在本地运行，请在 VS Code 中打开克隆的存储库，并在出现提示时选择 **Reopen in Container**。VS Code 将构建与 Codespace 相同的开发容器。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## 使用 GitHub Copilot Chat 和智能体模式

要在集成开发环境中使用 GitHub Copilot Chat 智能体模式，需要安装 GitHub Copilot Chat 扩展。使用 GitHub Codespace 时，该扩展通常已安装。

> [!TIP]
> 如果尚未安装 GitHub Copilot Chat 扩展，可以从 [Visual Studio Code Marketplace][copilot-chat-extension] 安装。也可以在 Visual Studio Code 中打开 Extensions 视图，搜索 **GitHub Copilot Chat** 并选择 **Install**。

安装扩展后，可能还需要使用 GitHub 账户进行身份验证。

1. 返回 Codespace。
2. 如果编辑器右侧未显示 Copilot Chat，请选择 Codespace 顶部的 **Copilot Chat** 图标。
3. 在 Copilot Chat 窗口中输入类似 “Hello world” 的消息并按 <kbd>Enter</kbd>，以启动 Copilot Chat。
4. 如果尚未完成身份验证，系统会提示登录 GitHub 账户。按提示完成身份验证。

   ![Copilot Chat 身份验证提示示例](../../../_images/ex1-copilot-authentication.png)

5. 完成身份验证后，Copilot Chat 窗口应会显示。

## 总结

你已创建实验存储库副本，并开始创建之后编写代码时要使用的 Codespace。

## 下一步

接下来让 Copilot 开始工作。继续学习[练习 1 - 自定义说明][next-lesson]，向 Copilot 介绍项目约定。

## 资源

- [GitHub Codespaces 概述][codespaces]
- [从模板创建存储库][template-repository]
- [开始使用 Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
