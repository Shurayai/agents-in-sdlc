---
title: "レッスン 7 - 品質保証 (QA) エージェントを作成して使う"
description: "Issue の要件、quality-checks スキル、Playwright MCP を組み合わせた QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright Model Context Protocol (MCP) でブラウザー上のフィルタリングを確認しました。ここでは、それらを明確な品質保証 (QA) 手順を持つカスタム エージェントにまとめます。

このレッスンでは、カスタム エージェントと指示、スキル、MCP ツールの連携を確認し、再利用可能な品質保証 (QA) プロファイルを作成して、フィルタリングの Issue に対する結果を確認します。

## シナリオとカスタム エージェント

Tailspin Toys では、プルリクエスト (PR) を作成する前に要件、コード品質、自動チェック、テスト範囲、ブラウザー上の動作を一貫して確認する必要があります。カスタム エージェントは QA の手順を調整し、再利用可能なレポートを作成できます。

カスタム エージェントは、目的、指示、利用可能なツールを定義した Markdown プロファイルです。このワークショップでは `.github/agents/qa.agent.md` に QA の役割を定義します。リポジトリの指示はチームの標準を示し、`quality-checks` スキルは繰り返し実行するチェックをまとめ、Playwright MCP はブラウザー ツールを提供します。QA プロファイルはこれらを使って要件を評価し、結果を報告します。

## QA プロファイルを作成する

実装コードを変更させずに、再利用可能な QA プロファイルを作成します。

1. Codespace に戻り、フィルタリングの会話が Interactive モードであることを確認します。
2. デフォルト エージェントに次のプロンプトを送信します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

QA エージェントを使う前に、意図した手順と制約が反映されていることを確認します。

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. フロントマターを確認します。`description` は必須で、`name` は任意ですが表示名として指定できます。
3. 要件から確認を始め、リポジトリの指示に従い、`quality-checks` スキルと Playwright MCP を使うことを確認します。
4. 根拠を示して報告し、実装コードを変更する前に確認を求め、コミットや PR 作成を行わないことを確認します。
5. 不足や制約の誤りがあれば、続行する前にデフォルト エージェントに修正を依頼します。

## Issue を QA エージェントで確認する

新しいエージェントは会話開始時に読み込まれるため、プロファイルを作成した後、同じフィルタリングの会話を再開します。

1. 次のコマンドで QA エージェントを有効にします。

   ```plaintext
   /agent QA
   ```

   作成直後は一覧に表示されない場合がありますが、このコマンドで有効にできます。

2. 次のプロンプトで機能をレビューするよう依頼します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. レポートを読み、各判定の根拠を確認します。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- カスタム エージェントと指示、スキル、MCP ツールの連携を確認しました。
- 再利用可能な品質保証プロファイルを作成して確認しました。
- QA エージェントを選択し、フィルタリング Issue に対する結果を確認しました。

再利用可能な専門エージェントを追加し、その作業をレビューしました。次は[機能 PR をまとめ、Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 用のカスタム エージェントを作成する][create-agents]
- [カスタム エージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
