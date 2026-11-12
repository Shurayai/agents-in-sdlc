---
title: "レッスン 2 - 星評価を追加する: 小さな改善"
description: "Copilot CLI でゲーム カードを変更し、転送ブラウザーで確認して、最初のプルリクエストをマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールして会話を試したので、プロジェクトに初めて変更を加えます。ゲームのデータには星評価がありますが、ホームページのゲーム カードには表示されていません。エージェントに評価を表示させ、変更を確認して、最初のプルリクエストとしてマージします。

このレッスンでは、次のことを行います。

- 機能ブランチで Copilot の会話を開始します。
- 小さな変更をエージェントに依頼します。
- `/diff` で変更をレビューします。
- 転送ブラウザーでアプリを実行して確認します。
- 最初のプルリクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、詳細ページにはすでに表示されています。ホームページのゲーム カードにはタイトル、カテゴリ、発行元、説明しか表示されません。ウォームアップとして、既存の評価を各カードに表示します。

## 会話の構成

**会話**は Copilot CLI でタスクに取り組む場所です。Copilot app と異なり、通常の CLI 会話では専用の worktree を作らず、ターミナルで現在チェックアウトしているリポジトリと Git ブランチを使います。保存した会話は後で再開できます。ファイルとブランチは通常の Git 状態としてディスク上に残ります。

会話では、プロンプトとエージェントの応答、ファイルを調べて編集するツールの操作、`/diff` で確認できる変更を扱います。

## 会話を開始して変更を依頼する

会話では Copilot CLI とタスクに取り組みます。通常の CLI 会話は、Copilot app のように専用 worktree を作るのではなく、ターミナルで現在チェックアウトしているリポジトリと Git ブランチを使います。

1. Codespace に戻ります。
2. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
3. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

4. スラッシュ コマンド `/new` を実行して <kbd>Enter</kbd> を押し、新しいセッションを開始します。
5. 次のプロンプトを送信します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot がプロジェクトを調べ、必要なファイルを特定して変更します。

## 差分をレビューする

マージする前に、AI が生成した変更をレビューします。

1. `/diff` を入力し、変更されたファイルをすべて確認します。
2. 評価がある場合に数値が表示され、`starRating` が `null` の場合に `No rating yet` と表示されることを確認します。
3. どちらの状態もテストされていることを確認します。
4. Copilot が実行したチェックの結果を確認し、失敗があれば修正を依頼します。
5. レビュー後、<kbd>Esc</kbd> を押して差分画面を終了します。

> [!NOTE]
> Copilot を含む生成 AI ツールは確率的に動作するため、コードは例と異なる場合があります。特定の実装ではなく、動作を確認してください。

## 変更を確認する

コードを読むだけでなく、Codespaces の転送ポートを使ってブラウザーでユーザー インターフェイス (UI) を確認します。

1. Copilot に次のプロンプトを送信します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces でポート `4321` が利用可能になったら、**Open in Browser** を選択します。
3. ゲーム カードに 5 段階の評価が表示されることを確認します。
4. Copilot に次のプロンプトを送り、起動したサーバーを停止します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初のプルリクエストを作成してマージする

確認した変更をプロジェクトにマージします。

1. エージェントに次のプロンプトを送り、変更をコミットします。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を実行します。Copilot CLI はプルリクエストの作成時に既存のコミットをプッシュし、URL を表示します。
3. Copilot CLI が表示した URL を、Mac では <kbd>Command</kbd>、Windows/Linux では <kbd>Ctrl</kbd> を押しながら選択して開きます。
4. 変更されたファイルとチェックをレビューします。
5. 準備ができたら **Merge pull request** を選択し、マージを確認します。
6. Codespace に戻り、`/exit` で Copilot CLI を終了します。
7. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- 機能ブランチで Copilot の会話を開始しました。
- エージェントにゲーム カードの小さな変更を依頼しました。
- `/diff` で変更をレビューしました。
- 転送ブラウザーでアプリを実行し、星評価を確認しました。
- 最初のプルリクエストを作成してマージしました。

Copilot CLI を使って最初の変更をリリースしました。

次は、[フィルタリングの Issue から始め、Plan と Autopilot モードを使って][next-lesson]より大きな機能を実装します。

## リソース

- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
