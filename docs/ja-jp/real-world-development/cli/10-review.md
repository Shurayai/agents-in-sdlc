---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys で一連の作業を行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトと用意されたフィルタリング Issue を確認しました。
- 星評価を追加し、転送ブラウザーで確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルタリング Issue から開始し、Plan モードで方針を決め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントをガイドし、`quality-checks` スキルを調整して単体テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルタリングを確認しました。
- 品質保証 (QA) カスタム エージェントを作成して選択し、要件、テスト範囲、スキルの結果、ブラウザーでの証拠を評価しました。
- フィルタリングの変更全体をレビューし、Agent Merge に PR の処理を許可しました。
- コンテキスト、モデル、共有、任意のクラウド委任に使うスラッシュ コマンドを確認しました。

## リリースした変更

ワークショップでは、更新済みの `main` から作成した別々のブランチで 2 つの PR を作成しました。

1. **星評価:** 既存の `starRating` と未評価の状態をゲーム カードに表示しました。
2. **フィルタリングと品質ワークフロー:** フィルタリングを実装し、指示を更新して機能に適用し、`quality-checks` のレポートを調整し、QA プロファイルと関連テストを追加しました。

フィルタリングの計画から PR 作成までは同じ会話とブランチを使いました。手順を簡潔にするため、作業を 1 つの PR にまとめています。

## 検証方法

自動テスト、自分で行うブラウザー確認、MCP 経由の Copilot によるブラウザー確認を組み合わせました。`quality-checks` スキルは単体テスト、lint、型チェックを実行し、新しい形式で報告しました。QA はこれらの結果に要件とテスト範囲のレビューを加えました。テストが本当の不足を補うようにし、QA 実行で追加テストが不要と判断される場合もあります。変更後はコードと証拠を再確認してください。

## ベスト プラクティス

Copilot に与えるコンテキストとツールが作業に影響します。このワークショップでは指示を更新し、スキルを調整し、QA プロファイルを作成し、MCP サーバーを構成しました。指示は標準を定め、スキルは反復可能な作業を示し、カスタム エージェントは専門の役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合った**モードとモデル**を選びます。**Plan** は実装前の検討、**Interactive** は変更を確認しながら進める作業、**Autopilot** は範囲が明確なタスクに使います。定型的な編集には高速なモデル、複雑な作業にはより高性能なモデルを選びます。何を、なぜ、どのように実現したいかを明確に伝えることも重要です。

## さらに試す

- `/review` でコードレビュー エージェントに変更を分析させます。
- `/rubber-duck` で問題を整理し、別の視点を得ます。
- `/fleet` で独立したサブタスクを並列に進めます。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを送ります。

## 次のステップ

ツールの使い方を上達させるには、実際の作業で使い続けることが大切です。チームと学んだことを共有し、互いの経験から学んでください。ターミナルから Tailspin Toys を拡張する場合は、任意の[Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境を試すには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を参照してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
