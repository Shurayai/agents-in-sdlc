---
title: "演習 3 - Playwright MCP サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: Agent mode][previous-lesson] · [次のレッスン: カスタム エージェント →][next-lesson]

Agent mode でフィルタリング機能を作成しました。プルリクエストを開く前に、ブラウザー上で実際に動作することを確認します。**Playwright MCP サーバー**を接続し、Copilot に実際のブラウザーを操作させて機能をテストします。その後、ブランチを公開して PR を作成します。

この演習では、Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを提供する仕組みを確認し、Playwright MCP サーバーをワークスペースに追加して、ブラウザーで手動テストを依頼します。また、ブランチを公開してフィルタリングの PR を作成します。

## Model Context Protocol (MCP) とは

Agent mode は、エディターの外部にあるツールを使えるとさらに便利です。MCP は、Copilot が外部ツールやサービスと通信するための標準です。

![Agent mode がコンテキスト、LLM、MCP サーバーや VS Code 拡張機能が提供するツールと連携する仕組みの図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) を使うと、AI エージェントはリソースを通じて最新情報にアクセスし、ツールを使って利用者に代わる操作を行えます。MCP サーバーはエージェントと外部サービスやツール (既存 API や NPM パッケージなどのローカル ツール) の橋渡しをし、利用可能なツールとリソースを管理します。

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)** は、GitHub リポジトリ、Issue、プルリクエストなどを管理する API を提供します。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)** は、Playwright によるブラウザー自動化機能を提供します。

そのほかのサーバーは、GitHub の [MCP レジストリ](https://github.com/mcp)で探せます。

> [!CAUTION]
> MCP サーバーはほかの依存関係と同様に扱ってください。使用前にソース コードと発行元を確認し、セキュリティへの影響を検討します。信頼できるサーバーのみを使い、機密リソースや操作へのアクセスを許可する際は注意してください。

## MCP の構成を確認する

`.vscode/mcp.json` は、JavaScript Object Notation (JSON) 形式で VS Code ワークスペースの MCP サーバーを設定します。

1. Codespace で `.vscode/mcp.json` を開きます。
2. すでに設定されている `github` サーバーを確認します。

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

この `github` エントリはプロジェクト テンプレートに含まれているため、前の演習で Copilot はバックログの Issue を読み取れました。[リモート GitHub MCP サーバー][remote-github-mcp-server]を使うので、ローカルにインストールする必要はありません。VS Code は HTTP で接続し、GitHub ツールを初めて使うときに認証を求めます。

## Playwright MCP サーバーを追加する

[Playwright MCP サーバー][playwright-mcp-server]を追加し、Copilot がブラウザーを操作して機能をテストできるようにします。

1. `.vscode/mcp.json` に `github` と並べて `playwright` エントリを追加します。

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

2. ファイルを保存します。

`github` はリモート サーバーですが、`playwright` はローカル サーバーです。VS Code が `npx @playwright/mcp@latest` を実行して起動します。`--headless` は画面を表示せずにブラウザーを実行するオプションです。Codespace には表示用デスクトップがないため必要です。

> [!NOTE]
> Tailspin Toys ではエンドツーエンド (E2E) テストに Playwright を使うため、ブラウザーはすでにインストールされていることが多いです。ブラウザーがないと Copilot が報告した場合は、`npx playwright install chromium` を実行して再試行します。

## サーバーを起動して信頼する

VS Code は MCP サーバーを必要に応じて起動します。Copilot がサーバーのツールを初めて使うとき、VS Code はサーバーを起動し、信頼を確認します。

1. `.vscode/mcp.json` の `playwright` エントリの上に表示される **Start** を選択し、サーバーを起動して構成を確認します。
2. VS Code が信頼を確認したら、構成をレビューしてサーバーを信頼し、起動を許可します。

手動で起動する必要はありません。省略した場合は、次の手順で Copilot がツールを初めて使うときにサーバーが起動し、信頼を確認されます。

## フィルタリング機能をテストする

Playwright MCP は、ブラウザーを開いてページを移動し、フィルターを適用し、結果を読み取れます。エージェントはスクリーンショットではなくページの[アクセシビリティ ツリー][playwright-mcp-server]を使います。ラベル付きのボタン、リンク、リスト項目などの構造を読み取るため、機能確認とあわせて基本的なアクセシビリティも確認できます。

サーバーを接続し、アプリを起動した状態で Copilot に次のプロンプトを送信します。

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot は Playwright MCP でブラウザーを起動し、各手順を試して結果を報告します。Issue の受け入れ条件に照らして報告を確認し、問題があれば PR を作る前に質問するか、コードの修正を依頼します。

> [!NOTE]
> テスト時にアプリが `http://localhost:4321` で実行されている必要があります。開発サーバーを停止した場合は、プロンプトを送る前に起動します。Playwright MCP の初回利用時にブラウザーのダウンロードが必要な場合があります。見つからないと報告されたら、`npx playwright install chromium` を実行して再試行します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプルリクエストを作成する

機能の動作を確認したので、チームがレビューできるよう `filtering-vscode` ブランチを公開します。

1. Codespace の **Source Control** パネルに移動し、Copilot の変更をレビューします。
2. **+** アイコンを選択して変更をステージします。
3. **Sparkle** ボタンでコミット メッセージを生成します。

   ![Copilot の変更が表示された Source Control パネル](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択してブランチをリポジトリにプッシュします。

## プルリクエストを作成する

PR は github.com や GitHub CLI から作成できますが、GitHub に接続済みの Copilot に依頼できます。

1. Copilot Chat パネルに移動し、**New Chat** を選択します。
2. エージェント ドロップダウンで **Agent** が選択されていることを確認します。
3. 次のプロンプトで PR の作成を依頼します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 情報の取得や操作を行うため **Continue** を求められたら選択します。GitHub ツールを初めて使う場合は GitHub 認証を求められることがあります。画面の指示に従います。
5. Copilot が Issue を検索し、PR を作成したことを確認します。
6. Copilot が生成したリンクを選択して PR をレビューします。まだマージしないでください。

## まとめと次のステップ

この演習では、次の作業を行いました。

- Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを提供する仕組みを確認しました。
- Playwright MCP サーバーをワークスペースに追加しました。
- ブラウザーでフィルタリング機能を手動でテストしました。
- ブランチを公開してフィルタリングのプルリクエストを作成しました。

次は[カスタム エージェントを作成し][next-lesson]、アクセシビリティ レビューなどの作業を効率化します。

## リソース

- [MCP とは何か、なぜ注目されているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
