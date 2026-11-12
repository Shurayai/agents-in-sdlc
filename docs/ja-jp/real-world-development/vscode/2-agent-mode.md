---
title: "演習 2 - Copilot Agent Mode で機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリの小さな更新でも、複数のファイル変更やテスト実行が必要になることがあります。必要なファイルを探し、変更し、テストし、失敗を調査して不足した修正を加える作業は続きます。Copilot Agent Mode は統合開発環境 (IDE) 内でより自律的に作業し、プロジェクトを調べ、必要なファイルを更新し、テストなどのタスクを実行し、見つかった問題を修正します。

> [!NOTE]
> 名前は似ていますが、agent mode と cloud agent は異なる用途です。Agent mode は IDE 内で作業し、素早く対話しながら進めます。Cloud agent はチーム メンバーのように非同期で作業し、Issue とプルリクエストを通してやりとりします。

この演習では、Copilot Agent Mode がプロジェクトを調べて関連ファイルを特定する方法、ユーザー インターフェイス (UI) とデータ層にまたがる機能の実装方法、マージ前に変更とテストをレビューする方法を確認します。

## シナリオ

ゲーム一覧が増えてきたため、カテゴリと発行元による絞り込みを追加します。前の演習で発行元ヘルパーを追加しました。残りのデータ層、UI、テストを Copilot Agent Mode で完成させます。

## Tailspin Toys の Web サイトを実行する

変更前に、現在のサイトの機能を確認します。Tailspin Toys は開発者をテーマにしたボード ゲームのクラウドファンディング サイトです。単一の Astro アプリで、ビルド時に静的な HyperText Markup Language (HTML) を生成します。ページは frontmatter から Drizzle ORM 経由でローカル SQLite データベースを直接参照します。別のバックエンド アプリケーション プログラミング インターフェイス (API) やクライアント ユーザー インターフェイス (UI) フレームワークはありません。データアクセス ヘルパーは `src/lib/` にあり、インタラクティブな動作には標準の Document Object Model (DOM) API を使う小さな Astro `<script>` を使います。

### Web サイトを起動する

`npm run dev` で Astro 開発サーバーを起動します。

1. 前の演習の後、`main` にいる Codespace に戻ります。
2. Codespace 内で <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押してターミナルを開きます。
3. フィルタリング用ブランチを作成します。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro 開発サーバーが起動すると、次のような URL が表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くダイアログが表示された場合は、**x** を選択して閉じます。

5. Mac では <kbd>Command</kbd>、Windows/Linux では <kbd>Ctrl</kbd> を押しながらターミナルの `http://localhost:4321` を選択してサイトを開きます。

> [!NOTE]
> Codespace のターミナルから localhost URL を選択すると、`https://<your-codespace-name>-4321.app.github.dev/` に転送されます。これは Codespace の Web サーバーへのプライベート トンネルです。

ホームページにはゲームのタイトル、画像、説明が一覧表示されます。ゲームを選択すると、タイトル、説明、発行元、カテゴリなどを含む詳細ページが表示されます。

## Copilot でバックログを確認する

テンプレートからプロジェクトを作成すると、Issue のバックログも作成されます。Copilot に一覧を表示してもらいます。

> [!TIP]
> **Copilot Chat を開く**
>
> Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。各演習で必要なモードとモデルは、その手順内で説明します。

1. Chat ビューのエージェント ドロップダウンから **Agent** を選択します。Agent は複数ファイルの変更を計画・実行し、ターミナル コマンドやツールを使います。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデルから **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このワークショップは特定モデルを推奨するものではありません。作成時に Claude Sonnet 4.5 を使い、比較的安定した体験を目指しています。大規模言語モデル (LLM) は確率的に動作するため、提案は例と異なる場合があります。これは想定された動作です。

> [!NOTE]
> 確率的な動作により、Copilot が別の MCP コマンドを使う場合がありますが、タスクは実行できるはずです。

3. 次のプロンプトを送信します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. Issue の一覧を取得するため **Continue** を選択します。
5. Issue の一覧と Copilot が提案した優先順位を確認します。

## 指示ファイルを確認する

コード生成を依頼する前に、Copilot にコンテキストを渡す `.github/instructions/ui.instructions.md` を確認します。

1. Codespace で `.github/instructions/ui.instructions.md` を開きます。
2. アーキテクチャの概要、コンポーネント設計・テスト可能性・アクセシビリティの原則、Astro、Tailwind CSS、Drizzle などの指示へのリンクを確認します。

> [!TIP]
> 指示ファイルから別の指示ファイルやプロジェクト ファイルを参照できます。パスは指示ファイルからの相対パスです。これにより、指示を再利用しやすい小さな単位に分け、例やテンプレートを示せます。

## フィルタリング機能を実装する

フィルタリングには、`src/lib/` のデータ層ロジック、動作を確認するテスト、ゲーム一覧ページの UI が必要です。Agent Mode にまとめて依頼します。

1. 現在の Copilot 会話を続けるか、**New Chat** で新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択します。

   ![UI 指示ファイルを選択する画面](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** であることを確認します。
5. 次のプロンプトを送信します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調べ、データ層、UI、テストを特定し、変更とテスト実行を行う様子を確認します。

   ![Copilot がプロジェクト ファイルを調べる画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトの調査、変更、テストを行うため、数分かかる場合があります。作業中、エディターに **Keep** と **Undo** が表示されることがあります。作業が終わるまで待ってください。完了後はすべての変更に対して選択できます。

7. Copilot に求められたら **Continue** を選択してテストを実行します。

   ![Copilot Chat でテスト実行の確認を求めるダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に停止したりテストが失敗したりしても、Copilot はコード生成とテストを繰り返します。

   ![Copilot Agent Mode の Chat セッションと提案された変更](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成コードに問題がないか確認します。

> [!CAUTION]
> Copilot などの AI ツールが生成したコードは、必ずレビューしてください。

10. サイトを開いているブラウザーに戻り、新機能を試します。
11. 動作とコードを確認した後、Copilot Chat で **Keep** を選択します。

## まとめと次のステップ

この演習では、次のことを確認しました。

- Copilot Agent Mode がプロジェクトを調べ、関連ファイルを特定し、複数ファイルにまたがる変更を調整する方法。
- GitHub Copilot Agent Mode で UI とデータ層にまたがる機能を実装する方法。
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューする方法。

Copilot Agent Mode を使って Tailspin Toys のサイトに機能を追加しました。次は[Playwright MCP サーバーで機能をテストし][next-lesson]、PR を作成します。

### おまけの演習 — ページネーションを実装する

ゲーム一覧が増えた場合に備えて、今回学んだ方法でページネーションを追加するよう Copilot に依頼できます。既存の指示ファイルに従い、ページ サイズを利用者が選択するか固定値にするかを決め、必要なコンテキストを含めてプロンプトを書きます。必要に応じて Copilot に追加変更や情報を伝えることも、通常の作業手順です。

## リソース

- [Copilot の ask、edit、agent mode: それぞれの役割と使い分け][choose-mode]
- [VS Code の agent mode][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
