---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

多くの組織は、未解決のセキュリティ問題、更新が必要なレガシ コード、バックログに残った機能要望などの技術的負債を抱えています。GitHub Copilot cloud agent はコードの更新や機能追加などを自律的に行います。作業が終わると、人間がレビューできるドラフトのプルリクエスト (PR) を作成します。時間のかかる作業を任せることで、開発者はより大きな課題に集中できます。

この演習では、Copilot cloud agent を使って次のことを行います。

- コード生成環境をカスタマイズします。
- 操作を安全に行う方法を確認します。
- Issue の範囲を明確にする重要性を確認します。
- Issue を Copilot に割り当てます。

## シナリオ

Tailspin Toys には、最初のサイトを開発した委託先が残した技術的負債があります。まず、アプリケーションのエクスポート関数すべてに TSDoc コメントを追加します。

さらにデザイン チームは、ゲームの詳細ページに同じカテゴリの別タイトルを表示して、ゲームを見つけやすくしたいと考えています。現時点では、UX の受け入れテストに使える実装が必要です。この作業は妨げになっていますが、優先度がより高い Issue もあります。どちらも後回しになりやすいタスクです。cloud agent に非同期で任せると、開発者は別の作業を進め、後から成果をレビューできます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent][copilot-agents] は、人間の開発者と同様にバックグラウンドで作業できます。たとえば[GitHub Issue を Copilot に割り当て][assign-issue]ると、進捗を追跡するドラフト PR を作成し、環境を設定して作業を始めます。セッションは実行中でも完了後でも確認でき、提案をレビューできる段階になると PR で通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot を使っても、考える作業を省略できるわけではありません。単純に見える作業も細部には複雑さがあります。[cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を明確にしてください。AI ペア プログラマーとして扱い、段階的に進め、学び、試し、調整します。生成 AI を加えてもソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習ではカスタム指示が Copilot をどうガイドするかを確認しました。まだ確認していない場合は、cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み取り専用で確認してください。

- `.github/copilot-instructions.md` を開き、特に TypeScript の規約と TSDoc コメントに関する **Code standards** を確認します。
- `.github/instructions/unit-tests.instructions.md` を開き、`applyTo` フロントマターが `**/*.test.ts` に指示を適用することを確認します。

次のセクションで `Code lacks documentation` Issue を割り当てたら、生成された PR の TSDoc コメント、TypeScript 規約、ファイル ヘッダーを確認します。これらは指示ファイルによるものです。

## cloud agent の開発環境を設定する

Copilot にタスクを割り当てる場合も、通常の開発と同じように環境の準備とスクリプト実行が必要です。cloud agent は GitHub Actions を使って環境を準備します。[特別なセットアップ ワークフロー][setup-workflow]を `.github/workflows/copilot-setup-steps.yml` に作成すると、作業前に必要なツールや依存関係を設定できます。このラボには、Node.js、プロジェクトの依存関係、エンドツーエンド (E2E) テスト用のブラウザー、単一 Astro アプリ用にマイグレーションとシードを行った SQLite データベースを準備するワークフローが設定済みです。

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

このファイルには、次のようなポイントがあります。

- `copilot-setup-steps` という 1 つのジョブがあり、Copilot が PR の作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` により、リポジトリの **Actions** タブから手動実行できます。Copilot の実行を待たずにワークフローをテストできます。

## ドキュメントを追加する Issue を割り当てる

ドキュメントの不足は、生産性を下げ、コードベースの保守や新しい開発者の参加を難しくする技術的負債です。Copilot cloud agent に Issue を割り当て、バックグラウンドでドキュメントを作成させます。後の演習で成果をレビューします。

1. 新しいブラウザー タブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次のテキストを入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. **Create** を選択します。
8. 右側の **Assign to Copilot** を選択します。

   ![Issue に Copilot を割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. 新しく作成された PR を開きます。タイトルは `[WIP]: Code lacks documentation` などです。表示されない場合は少し待ってからブラウザーを更新します。
12. 数分後、Copilot が TODO リストを作成したことを確認します。

> [!NOTE]
> TODO リストの表示には数分かかる場合があります。Copilot が環境を準備し、プロジェクトを分析して、作業方法を決めています。

13. TODO リストと実行予定のタスクを確認します。
14. PR のタイムラインを下に移動し、Copilot が Issue の作業を開始したことを確認します。
15. **View session** を選択します。

   ![Copilot セッションを表示する画面](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新されたインジケーターを表示するために、ブラウザーを更新する必要がある場合があります。

16. ライブ セッションを確認します。Copilot がコードを調べて状態を理解し、計画を決め、コードを作成する様子を確認します。

作業には数分かかる場合があります。cloud agent の利点は、非同期に作業を任せられることです。別の Issue も割り当て、その間にアプリの機能を実装します。

## ゲーム詳細ページに関連ゲームを追加する

cloud agent に作業を分けて任せることで、別のタスクを進められます。デザイン チーム向けの関連ゲーム機能も Copilot に割り当てます。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択します。
4. 空のテンプレートとして **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次のテキストを入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create** を選択します。
8. 右側の **Assign to Copilot** を選択します。

   ![Issue に Copilot を割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

Issue の最初のコメントに 👀 が表示されると、Copilot が作業を開始したことを示します。

![Copilot が Issue で作業中であることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot が 2 つ目の依頼に取り組んでいる間、完了後に結果をレビューできるようにしておきます。次はカスタム エージェントを作成して使います。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents]を使い、Issue を割り当てて非同期に作業させる方法を確認しました。技術的負債への対応、新機能の作成、フレームワーク間のコード移行などを任せられます。

この演習では、次のことを確認しました。

- コード生成環境をカスタマイズする方法。
- 操作を安全に行う方法。
- Issue の範囲を明確にする重要性。
- Issue を Copilot に割り当てる方法。

次はカスタム エージェントを作成して使います。cloud agent は [Model Context Protocol (MCP) サーバー][cloud-agent-mcp]とカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
