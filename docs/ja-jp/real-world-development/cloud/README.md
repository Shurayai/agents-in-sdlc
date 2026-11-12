---
slug: ja-jp/real-world-development/cloud
title: "GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent) は、GitHub Copilot がクラウドで非同期に作業できる機能です。GitHub で作業を割り当てると、cloud agent はバックグラウンドでリポジトリを調べ、変更を加えてプルリクエストを作成します。その間、別の作業を続けられます。

この演習では、cloud agent が従うカスタム指示を追加し、GitHub Issue を割り当てて実装を依頼します。カスタム エージェントを確認して利用し、エージェントのダッシュボードからセッションを監視して方向を調整した後、プルリクエストをレビューして成果を改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. カスタム指示][ex1] | コンテキスト | cloud agent が従うカスタム指示を追加します |
| [2. Cloud agent][ex2] | 非同期エージェント | GitHub Issue を Copilot cloud agent に割り当てます |
| [3. カスタム エージェント][ex3] | 特化型エージェント | カスタム エージェントを確認して利用します |
| [4. エージェントの管理][ex4] | 監視 | エージェント セッションを監視して方向を調整します |
| [5. 反復][ex5] | レビュー | プルリクエストをレビューし、Copilot の作業を改善して次の手順を選びます |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** プランを利用できる GitHub アカウント
- [ ] アカウントまたは組織で有効になっている Copilot cloud agent

> [!TIP]
> 有料プランを利用していない場合、認定済みの学生は[GitHub Education][callout-student-plan-education]から GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI が含まれているため、すべてのハーネスを完了できます。

[callout-student-plan-education]: https://github.com/education/students

> [!NOTE]
> Cloud agent は Copilot Free を除く **Copilot Student、Pro、Pro+、Business、Enterprise** で利用できます。Copilot Business または Enterprise では、管理者が組織で有効にする必要があります。

> [!NOTE]
> このハーネスでは Model Context Protocol (MCP) を扱いません。Copilot で MCP サーバーを使う方法については、[CLI ハーネス](../cli/)または [VS Code ハーネス](../vscode/)を参照してください。

## 開始する

**[演習 0: 前提条件から開始する →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-cloud-agent/
[ex3]: 3-custom-agents/
[ex4]: 4-managing-agents/
[ex5]: 5-iterating/
