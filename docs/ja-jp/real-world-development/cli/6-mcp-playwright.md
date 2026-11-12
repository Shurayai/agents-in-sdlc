---
title: "レッスン 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI で Playwright MCP を確認または構成し、ブラウザーでフィルタリング機能を試します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

コードを書くこと以外にも、データや外部サービスを使ったり、Copilot で追加ツールを利用したりする作業があります。Model Context Protocol (MCP) サーバーを使うと、Copilot CLI に組み込まれていないツールやサービスを利用できます。

このレッスンでは、MCP の概要と Copilot CLI での利用方法を確認し、Playwright MCP サーバーがまだ利用できない場合は追加して、エージェントにブラウザー操作を依頼します。

## シナリオ

UI の変更を検証するには、実際に操作する必要があります。Copilot が開発中のサイトをユーザーのように操作できるようにし、期待どおりの動作を確認します。

## MCP とは

[Model Context Protocol (MCP)][mcp-blog-post] は、人工知能 (AI) エージェントが外部のツールやサービスと通信するための仕組みです。MCP サーバーはエージェントと外部ツールの橋渡しをし、利用できるツールやリソースを提供します。たとえば、[GitHub MCP Server][github-mcp] はリポジトリ、Issue、プルリクエストを管理するアプリケーション プログラミング インターフェイス (API) を提供し、[Playwright MCP Server][playwright-mcp-server] は Playwright によるブラウザー自動化機能を提供します。[MCP レジストリ][mcp-registry]では、ほかのサーバーも探せます。

> [!CAUTION]
> MCP サーバーはほかの依存関係と同じように扱ってください。使用前にソース コードと発行元を確認し、セキュリティへの影響を検討してください。

## Playwright MCP サーバーを追加する

Copilot CLI で Playwright MCP がすでに構成されている場合は、セットアップを飛ばして次のセクションに進みます。

1. Codespace に戻ります。
2. Copilot CLI で `/mcp add` を実行します。
3. 名前に `playwright` と入力して <kbd>Tab</kbd> を押します。
4. サーバーの種類が **STDIO** であることを確認し、<kbd>Enter</kbd>、次に <kbd>Tab</kbd> を押します。
5. **Command** ダイアログに次のコマンドを入力します。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) で保存します。
7. <kbd>Esc</kbd> を押して MCP ダイアログを閉じます。

## Playwright で機能を確認する

以前は手動で機能を確認しました。ここでは Playwright MCP を使って同じ確認を行います。

1. Copilot に次のプロンプトを送信します。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

2. Copilot がブラウザーで機能を確認する手順を確認します。
3. 結果を読み、すべて期待どおりに動作していることを確認します。

> [!NOTE]
> 通常 Copilot は必要な MCP サーバーを自分で判断するため、プロンプトでサーバー名を指定する必要はありません。使うサーバーが分かっている場合は明示すると、結果の一貫性を高め、トークンを節約できます。

Copilot はアプリを起動し、Playwright で操作し、サーバーを停止して結果を報告します。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- MCP と Copilot CLI での利用方法を確認しました。
- Playwright MCP サーバーが未設定の場合に追加しました。
- エージェントにブラウザーを操作させ、フィルタリング機能を確認しました。

Copilot CLI から Playwright MCP を使ってブラウザーで機能を確認しました。次は[QA カスタム エージェントを作成し][next-lesson]、スキルとブラウザー ツールを組み合わせます。

## リソース

- [MCP とは何か][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
