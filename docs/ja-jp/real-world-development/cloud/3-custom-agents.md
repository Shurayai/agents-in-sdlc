---
title: "演習 3 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]を使うと、開発ワークフローの特定のタスクや分野に合わせた人工知能 (AI) アシスタントを作成できます。リポジトリの `.github/agents` にある Markdown ファイルで、指示、ベスト プラクティス、コーディング パターン、分野固有の知識を定義します。チームの専門知識を再利用可能なエージェントにまとめることで、たとえば Web Content Accessibility Guidelines (WCAG) に準拠する[アクセシビリティ エージェント][wcag]、安全なコーディングを行うセキュリティ エージェント、一貫したテスト パターンを守るテスト エージェントを作成できます。

カスタム エージェントはプロジェクト内の `.github/agents`、またはユーザー全体の `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには少なくとも `name` と `description` を含む YAML (YAML Ain't Markup Language) フロントマターと、エージェントの動作、専門知識、指示を記載する Markdown プロンプトが必要です。

### カスタム エージェントとエージェント スキルの違い

[エージェント スキル][agent-skills-concept]とカスタム エージェントには共通点があります。どちらも主に Markdown ファイルで定義し、AI に作業方法を伝えます。大まかに言うと、**カスタム エージェントは作業者、スキルはツール**です。

カスタム エージェントは独自のコンテキスト ウィンドウを持ち、スキルやほかのエージェントを調整します。このラボのアクセシビリティ カスタム エージェントは、ガイドラインに沿ってサイトをレビューし、更新します。その作業の一部として、プルリクエスト ワークフローやテスト実行のスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成に唯一の正解はありません。ほかの AI の使い方と同じように、環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

この演習では、カスタム エージェントの定義方法と、タスクの割り当て方を確認します。

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず誰もが利用できるクラウドファンディング プラットフォームを目指しています。現在のダーク テーマはテキストと背景のコントラストが十分でなく、読みにくいというフィードバックがありました。デザイン チームは、利用者が切り替えられる高コントラスト モードを求めています。アクセシビリティは重要なので、カスタム エージェントに機能を実装させます。

## アクセシビリティ カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントは作成済みです。指示内容を確認します。

1. Codespace に戻り、`.github/agents/accessibility.md` を開きます。
2. `name` と `description` を含む YAML フロントマターを確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` のフロントマターが必要です。

3. 続くセクションを読み、アクセシブルな Web サイトのコード生成に関する主要な責務、ベスト プラクティス、HTML・CSS・JavaScript のコード例、よくある問題を確認します。

## Issue を作成して割り当てる

Copilot のすべてのエージェントを管理できる場所が Mission Control です。Issue を割り当てて、高コントラスト モードを実装させます。

1. リポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue**、次に **Blank issue** を選択します。
4. **Title** に `Add high contrast mode to website` と入力します。
5. **Description** に次のテキストを入力します。

   ```plaintext
   We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
   ```

6. **Create** を選択します。
7. 右側の **Assign to Copilot** を選択します。
8. 一覧から **Accessibility agent** を選択します。

   ![カスタム エージェントに Accessibility が選択されている cloud agent 割り当て画面](../../../_images/ex5-select-custom-agent.png)

9. **Assign** を選択します。

Copilot はバックグラウンドで作業を開始します。

## まとめと次のステップ

[GitHub Copilot のカスタム エージェント][custom-agents]を確認しました。カスタム エージェントは特定のタスクや分野に合わせた専門 AI アシスタントです。チームの専門知識や標準を再利用可能なエージェントにまとめられます。

この演習では、次のことを確認しました。

- カスタム エージェントの定義方法。
- カスタム エージェントへのタスクの割り当て方。

高コントラスト モードの実装を Copilot に任せ、次は Mission Control で[セッションを監視して方向を調整します][next-lesson]。

## リソース

- [カスタム エージェントについて][custom-agents]
- [組織でカスタム エージェントを使うための準備][org-custom-agents]
- [エンタープライズでカスタム エージェントを使うための準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
