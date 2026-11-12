---
title: "レッスン 5 - quality-checks スキルをカスタマイズして使う"
description: "既存の quality-checks スキルを確認し、レポート形式をカスタマイズして、フィルタリング機能を検証します。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くこと以外にも、手動で動作を確認したり、指示ファイルで規約に従わせたりできます。テストや lint、継続的インテグレーション (CI) のほかの作業には、**エージェント スキル**が適しています。スキルは、こうした作業の実行方法を Copilot に伝えます。

このレッスンでは、次のことを行います。

- 既存の `quality-checks` スキルを確認します。
- 結果のレポート形式をカスタマイズします。
- スキルを再読み込みして実行します。

## シナリオ

Tailspin Toys は単体テスト、lint、型チェックに `quality-checks` スキルを使います。チームは、実行結果を読みやすくするためにレポートを改善したいと考えています。

## 指示、スクリプト、リソース

エージェント スキルは、再利用可能なタスク指示、実行可能なスクリプト、補助リソースをまとめ、必要なときにエージェントが読み込みます。スキルはその名前のフォルダーと `SKILL.md` で構成されます。Markdown には、スキルの名前と説明を定義するフロントマター、機能の概要、呼び出すタイミングの指針を記載します。必要に応じてスクリプトやほかのリソース用のサブフォルダーを追加できます。

> [!NOTE]
> スキルに追加のファイルやフォルダーは必須ではありません。Tailspin Toys の `quality-checks` スキルには `SKILL.md` しかありません。プロジェクトにある既存コマンドを使うためです。

スキルは、チームで共有して再利用するリポジトリの `.github/skills`、またはユーザー用の `~/.copilot/skills` に配置できます。

## スキルを確認する

Tailspin Toys チームが単体テスト、lint、型チェックを実行するために作成した `quality-checks` スキルを確認します。

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 先頭の `name` と `description` を読みます。説明によって、Copilot はスキルを呼び出すタイミングを判断します。
3. 指示を読み、テストと lint の手順をどのようにガイドしているか確認します。
4. **Results output formatting** セクションがまだないことを確認します。

## 変更前にスキルを実行する

Copilot CLI では、スキルを直接呼び出すか自然な言葉で依頼できます。スキルに 3 つのチェックを実行させます。

1. Interactive モードのフィルタリング会話に戻ります。
2. 次のプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認します。

## レポートをカスタマイズする

何を実行したか、成功したか、ツールが実際に何を報告したかが分かるようにレポートを改善します。

1. `.github/skills/quality-checks/SKILL.md` を開きます。
2. ファイルの末尾に次のセクションを追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルを保存します。変更は自動的に保存されます。

## 更新したスキルを実行する

Copilot CLI は会話を再起動せずに、編集されたスキルを再読み込みできます。

1. 次のコマンドを入力します。

   ```plaintext
   /skills reload
   ```

2. 先ほどと**同じプロンプト**を送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認し、最初のレポートと比較します。

## まとめと次のステップ

既存のエージェント スキルをカスタマイズして使用しました。

- 単体テスト、lint、型チェックに使う `quality-checks` スキルを確認しました。
- 結果のレポート形式をカスタマイズしました。
- スキルを再読み込みして実行しました。

この変更はフィルタリング機能のプルリクエスト (PR) に含めます。次は[Playwright Model Context Protocol (MCP) サーバー][next-lesson]を通じて、Copilot がサイトを直接操作できるようにします。

## スキルの例

コミュニティの次の例は参考資料であり、追加作業ではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューション ワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とエクスポート スクリプト: `drawio`][drawio-example]
- [ブラウザー テスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
