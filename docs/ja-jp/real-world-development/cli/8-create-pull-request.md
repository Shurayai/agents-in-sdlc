---
title: "レッスン 8 - 機能 PR を作成してマージする"
description: "フィルタリング機能と検証結果をレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルタリングの実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストは同じブランチに保存されています。まとめてレビューし、プルリクエスト (PR) を作成します。星評価の PR は手動でマージしましたが、今回は **Agent Merge** にマージの作業を任せます。

このレッスンでは、Agent Merge による PR ライフサイクルの自動化を確認し、機能変更全体と検証結果を調べ、フィルタリング PR を作成します。レビュー後に Agent Merge を有効にし、PR がマージされたことを確認します。

> [!NOTE]
> 通常は機能、指示、スキル、QA エージェントを複数の PR に分けます。このワークショップでは手順を簡潔にするため、フィルタリングと品質確認の作業を 1 つの会話とブランチにまとめています。

## Agent Merge について

**Agent Merge** は PR をマージするために必要な作業を自動化します。有効にすると、失敗した継続的インテグレーション (CI) チェックの修正、レビューコメントへの対応、必要なリベースなどを行い、リポジトリが許可していれば GitHub の自動マージを有効にします。Agent Merge を有効にする前に、変更をレビューして準備ができていることを判断してください。

## Agent Merge で PR を管理する

すべての変更を確認し、PR を作成してから Agent Merge を有効にします。

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. 一覧から **Default** を選択して <kbd>Enter</kbd> を押します。
4. `/pr create` を実行して PR を作成します。
5. `/pr agentmerge` を実行して Agent Merge を有効にします。
6. Copilot が PR の CI を監視し、すべて成功した後にマージすることを確認します。
7. Copilot から `PR #14 was squash-merged successfully.` のようなメッセージが表示されたことを確認します。

> [!IMPORTANT]
> Agent Merge は必須の承認、ブランチ保護、マージ キュー、リポジトリ設定、権限の不足を回避しません。ブロックされた場合は理由を確認し、リポジトリで許可されている場合はレビュー済みの PR を手動でマージします。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- Agent Merge と PR ライフサイクルの自動化について確認しました。
- 機能変更全体と検証結果を確認しました。
- フィルタリング PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR がマージされたことを確認しました。

コードの生成、テストと検証、PR の処理を自動化しました。次は[Copilot CLI の便利なスラッシュ コマンド][next-lesson]を確認し、コンテキスト、モデル、共有、任意のクラウドへの委任を試します。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
