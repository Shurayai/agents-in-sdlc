---
title: "演習 4 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に合わせた人工知能 (AI) アシスタントを作成できます。リポジトリの `.github/agents` にある Markdown ファイルで、エージェントの指示、ベスト プラクティス、コーディング パターン、分野固有の知識を定義します。たとえば、[Web Content Accessibility Guidelines (WCAG)][wcag] に準拠するアクセシビリティ エージェント、安全なコーディングを行うセキュリティ エージェント、一貫したテスト パターンを守るテスト エージェントを作成できます。

カスタム エージェントはプロジェクト内の `.github/agents`、またはユーザー全体の `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには少なくとも `name` と `description` を含む YAML (YAML Ain't Markup Language) フロントマターと、動作、専門知識、指示を記載する Markdown プロンプトが必要です。

### カスタム エージェントとエージェント スキルの違い

[エージェント スキル][agent-skills-concept]とカスタム エージェントには共通点があります。どちらも主に Markdown ファイルで定義し、AI に作業方法を伝えます。大まかに言うと、**カスタム エージェントは作業者、スキルはツール**です。

カスタム エージェントは独自のコンテキスト ウィンドウを持ち、スキルやほかのエージェントを調整します。このラボのアクセシビリティ カスタム エージェントは、ガイドラインに沿ってサイトをレビューし、更新します。その作業の一部として、プルリクエスト ワークフローやテスト実行のスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成に唯一の正解はありません。環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず誰もが使えるクラウドファンディング プラットフォームを目指しています。現在のダーク テーマはテキストと背景のコントラストが十分でなく、読みにくいというフィードバックがありました。デザイン チームは、利用者が切り替えられる高コントラスト モードを求めています。この演習ではカスタム エージェントに機能を実装させます。

この演習では、既存のアクセシビリティ カスタム エージェントを確認し、Copilot Chat で使って高コントラスト モードを実装します。

## アクセシビリティ カスタム エージェントを確認する

フィルタリング PR とは分けてアクセシビリティ作業を行うため、`main` から新しいブランチを作成します。

1. Codespace に戻り、ターミナルを開きます。
2. `main` を更新し、ブランチを作成します。

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

3. `.github/agents/accessibility.md` を開きます。
4. `name` と `description` を含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` のフロントマターが必要です。

5. 続くセクションを読み、アクセシブルな Web サイトのコード生成に関する主要な責務、ベスト プラクティス、HyperText Markup Language (HTML)、カスケーディング スタイル シート (CSS)、JavaScript のコード例、よくある問題を確認します。

## Copilot Chat でカスタム エージェントを使う

VS Code の Copilot Chat ビュー下部にあるエージェント ドロップダウンには、`.github/agents` に定義したカスタム エージェントが表示されます。エージェントを選択すると、その指示とツールに合わせたセッションになります。

> [!TIP]
> **Copilot Chat を開く**
>
> Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習によって異なります。必要な場合は各手順で説明します。

1. Chat ビューのエージェント ドロップダウンから **Agent** を選択します (まだ選択されていない場合)。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. Chat ビュー下部のエージェント ドロップダウンを選択します。既定では **default** が選択されています。
3. 一覧から **Accessibility agent** を選択します。
4. 次のプロンプトを送信します。

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

5. Copilot Chat がコードベースを調べ、変更を提案してプロジェクト ファイルを編集する様子を確認します。編集はファイル パスと差分とともに Chat に表示されます。
6. 編集が追加されると、エージェントが変更した作業セットを示す **Files changed** の表示が更新されます。

> [!NOTE]
> 作業には数分かかる場合があります。Copilot は Astro コンポーネント、CSS、関連テストなどの既存ファイルを変更することがあります。

次の演習では、作業中のセッションをレビューし、方向を調整します。

## まとめと次のステップ

[カスタム エージェント][custom-agents]が特定のタスクや分野に合わせた専門 AI アシスタントであることを確認しました。チームの専門知識や標準を再利用可能なエージェントにまとめられます。この演習では、カスタム エージェントの定義と、Copilot Chat の agent mode での利用方法を確認しました。

この演習では、次のことを行いました。

- 既存のアクセシビリティ カスタム エージェントを確認しました。
- Copilot Chat の agent mode でアクセシビリティ エージェントを使いました。

次は[エージェントの作業を監視して方向を調整し][next-lesson]、変更を確認しながら同じセッションにライト モードの切り替えを追加します。

## リソース

- [カスタム エージェントについて][custom-agents]
- [IDE でカスタム エージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタム エージェント][custom-agents-vscode]
- [カスタム エージェントの構成][custom-agents-config]
- [awesome-copilot のカスタム エージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP サーバーで機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
