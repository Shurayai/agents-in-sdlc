---
title: "第 4 课 - 使用自定义说明指导 Copilot"
description: "探索存储库说明、添加文档标准，并将其应用于过滤功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式人工智能（AI）时，上下文至关重要。如果任务需要以特定方式完成，应让 Copilot 能够获取相关指导。[说明文件][instruction-files]不仅描述想要什么代码，还说明代码应如何组织。现在过滤功能已构建完成，你将探索 Copilot 使用的说明、添加一项文档标准并将其应用于代码。

在本课中，你将：

- 了解存储库说明和按路径限定范围的说明文件如何传递给智能体。
- 更新说明文件，确保遵循编码标准。
- 观察说明文件对代码的影响。

## 场景

Tailspin Toys 有一套开发实践准则和要求，包括：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值，并在适用时说明可注入的 `db` 参数。
- 可复用 Astro 组件应说明其 `Props` 接口，相关代码更改时也应更新注释。
- 保留现有格式和 lint 指导。

通过说明文件，可以让 Copilot 获取正确的信息，并按照这些实践要求完成任务。

## 说明文件

自定义说明可向 Copilot 提供上下文和偏好，帮助它理解编码风格和需求。可以指定编码约定、库以及注释风格，也可以为整个存储库或特定文件类型创建说明，提供任务级上下文。

说明文件分为两类：

- `.github/copilot-instructions.md`：面向整个存储库的单个说明文件，会随该存储库的**每个**请求发送给 Copilot。文件应包含对大多数请求都适用的项目级信息。
- `.github/instructions/*.instructions.md`：为特定语言、文件类型或任务提供指导。

> [!NOTE]
> 其他说明格式及其支持情况因环境而异。依赖某种格式前，请查阅[自定义说明支持参考][custom-instructions-support]。

## 探索项目中的自定义说明文件

初始项目已包含一组说明文件。先探索现有内容，再进行更改，以便观察其影响。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（而不是终端）中打开 `.github/copilot-instructions.md`。
3. 浏览项目简介和编码指导。此文件适用于在此存储库中与 Copilot 的所有交互。
4. 打开 `.github/instructions` 文件夹并浏览其中的文件。这里有针对 Astro 文件、Drizzle 数据层、测试等内容的说明。
5. 打开 `.github/instructions/unit-tests.instructions.md`。注意顶部的 `applyTo` 字段，它指定了这些说明适用于哪些文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看它指向的其他说明文件和项目文件。这种做法可将较大的说明集拆分成更小、可复用的文件，并为 Copilot 提供参考示例。

## 更新说明文件以符合团队指导

虽然现有文件已是良好起点，但仍有缺漏。现在修改核心的 `copilot-instructions.md`，要求为新生成的 TypeScript 添加 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，该部分应位于第 35 行附近。
2. 在该部分末尾添加以下项目：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 应用更新后的指导

Copilot CLI 会在对话启动时加载存储库说明。保存更新后，退出并恢复过滤功能对话，让 Copilot 在保留功能上下文的同时加载新指导。

1. 如果过滤功能对话仍处于打开状态，输入 `/exit` 退出。Copilot CLI 会自动保存对话。
2. 在 `game-filters-cli` 分支的存储库根目录中恢复已保存的对话：

   ```bash
   copilot --resume
   ```

   如果出现提示，请选择过滤功能对话，并确认当前检出的是 `game-filters-cli` 分支。
3. 请 Copilot 应用更新后的指导：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff` 并检查已更改的 TypeScript 文件。查看新添加的 TSDoc 注释，并确认其准确说明了代码。

## 总结和后续步骤

你探索了 Copilot CLI 如何读取说明文件中的上下文，并将新的标准应用于功能代码。具体来说，你：

- 探索了存储库说明和按路径限定范围的说明文件。
- 更新了说明文件，确保遵循编码标准。
- 观察了说明文件对代码的影响。

接下来，[自定义并运行可复用的 quality-checks 技能][next-lesson]，以一致的方式运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义说明][instruction-files]
- [自定义说明支持][custom-instructions-support]
- [创建自定义说明的最佳实践][instructions-best-practices]
- [Awesome Copilot——说明文件及其他资源][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
