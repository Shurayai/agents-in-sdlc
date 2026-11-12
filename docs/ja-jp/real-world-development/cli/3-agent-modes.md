---
title: "レッスン 3 - エージェント モード: Plan と Autopilot"
description: "Plan で方針を決め、Autopilot で Issue に基づくフィルタリングを実装し、Interactive モードで結果を確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

小さな機能を追加したので、次はより堅実な手順で大きな変更に取り組みます。このレッスンでは、Issue から機能を実装し、コードの妥当性と動作を確認して、プロジェクトにマージする開発フローを体験します。

> [!NOTE]
> 機能の作業を続ける間、同じ会話とブランチを使います。通常はファイルの種類ごとにブランチやプルリクエストを分けますが、ここでは主要な概念に集中するため手順を簡略化します。

このレッスンでは、次のことを行います。

- GitHub Issue から Copilot の会話を開始します。
- Plan モードで要件を決めます。
- Autopilot モードで機能を実装します。
- コードをレビューします。
- 転送ブラウザーで機能を手動で確認します。

この機能の作業は次のレッスンにも続きます。リポジトリの指示を更新し、既存の `quality-checks` スキルをカスタマイズし、MCP による検証を追加して QA エージェントを作成した後、機能のプルリクエストを開きます。

## シナリオ

Tailspin Toys のカタログが増え、訪問者がカテゴリと発行元でゲームを絞り込める必要があります。Issue には機能が記載されていますが、カテゴリを組み合わせる方法など、実装前に合意すべき点があります。Plan モードで決定し、範囲を明確にしてから Autopilot に実装を任せます。

人工知能 (AI) エージェントを使っても、開発の基本は変わりません。一般的な流れは、Issue から始め、計画を立て、実装とレビューを行い、テストと手動確認をして、プルリクエストを作成し、レビューと継続的インテグレーション (CI) の成功後にマージすることです。チームによって細部は異なりますが、生成コードにも通常の確認手順を適用します。

## 会話モード

会話モードは、エージェントにどの程度の自律性を与えるかを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> でモードを切り替えます。

- **Interactive**: エージェントが変更を提案し、開発者の入力を待ちます。
- **Plan**: エージェントが計画を作成します。プロジェクト ファイルは編集できません。
- **Autopilot**: エージェントがコードを書き、テストを実行し、タスクが完了するまで反復します。

まず Plan モードで計画を確認し、その後 Autopilot で実装します。

## Issue から開始する

Codespace とリポジトリを準備し、フィルタリング用のブランチを作成します。

1. Codespace に戻ります。停止している場合は再起動します。
2. 星評価のプルリクエストがマージ済みであることを確認します。
3. ターミナルが開いていない場合は、<kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押します。
4. `main` を更新してブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

6. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
7. <kbd>A</kbd> を押してすべての Issue を表示します。
8. 矢印キーで **Allow users to filter games by category and publisher** という Issue を選択します。
9. <kbd>C</kbd> を押して Issue をプロンプトに追加し、**Session** タブに戻ります。

プロンプトに `#7` (または同様の番号) が追加されます。`#` を使うと GitHub の Issue やプルリクエストをコンテキストに含められます。

## フィルタリング機能を計画する

計画を立てることで、実装前に機能の方針を決められます。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Plan モードに切り替え、プロンプト下部に **Plan** と表示されることを確認します。
2. Issue の参照に続けて、次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

3. フィルタリングの動作について質問されたら、希望する動作を回答します。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して展開します。
5. 計画を読み、決定と異なる部分があれば修正を依頼します。

## Autopilot を承認する

計画を確認した後、実装を開始します。

1. **Accept plan and build on autopilot (recommended)** またはインストール済みバージョンで同様のラベルの項目を選択します。
2. プロンプト下部に **Autopilot** と表示されることを確認します。
3. Copilot が計画に沿ってコードを生成し、テストを実行する様子を確認します。

> [!NOTE]
> 承認すると実装がすぐに始まる場合があります。先に計画を確認してください。依存関係不足やポート競合が報告された場合は、チェック完了と判断する前に環境の問題を解決します。

## 実装をレビューして検証する

生成されたコードをレビューし、アプリを起動して動作を確認します。

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替えます。
2. `/diff` を入力し、フィルタリングの実装とテストを確認します。
3. 変更を Issue と計画上の決定に照らして確認します。
4. <kbd>Esc</kbd> を押して差分表示を終了します。
5. プロジェクトのチェック結果を確認し、失敗があれば修正を依頼します。
6. Copilot に次のプロンプトを送信します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

7. Codespaces でポート `4321` が利用可能になったら、**Open in Browser** を選択します。
8. 計画で決めたカテゴリと発行元の絞り込みや組み合わせを試します。
9. リセットと結果がない場合の動作が、Issue と決定に合っていることを確認します。
10. Codespace に戻り、Copilot に起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- GitHub Issue から Copilot の会話を開始しました。
- Plan モードで要件を決めました。
- Autopilot モードで機能を実装しました。
- コードをレビューしました。
- 転送ブラウザーで機能を手動で確認しました。

会話モードを使い分けて機能を実装し、レビューしました。次は[カスタム指示を使って][next-lesson]、コードが文書化された規約に従うようにします。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
