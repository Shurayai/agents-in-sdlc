---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成したアプリケーション、共有バックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を活用します。変更の計画、コード作成、動作確認、プルリクエストのレビュー、エージェントを使った作業管理を反復的に行います。

## シナリオ

開発者として、ボードゲームのクラウドファンディングを提供する架空の会社 Tailspin Toys に参加します。チームのバックログは GitHub Issue として用意されており、すぐに作業を始められます。カテゴリやページネーションの機能に加え、アクセシビリティやコーディング標準などの品質改善も含まれます。

## 作業環境を選ぶ

GitHub Copilot は、さまざまな作業環境で利用できます。開発方法に合った環境を選んでください。各ワークショップでは個別にセットアップを行い、Tailspin Toys のシナリオを共通して使います。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使います。Plan と Autopilot モード、指示、スキル、カスタム エージェント、Playwright Model Context Protocol (MCP)、Agent Merge、便利なスラッシュ コマンドを試します。

### [GitHub Copilot app][app]

デスクトップ アプリでエージェント セッションを並行して実行し、セッション モードを切り替え、Canvas で共同作業し、GitHub Issue とプルリクエストを管理します。

### [GitHub Copilot cloud agent][cloud]

GitHub Issue を非同期エージェントに割り当て、作業をガイドして進行状況を監視し、作成されたプルリクエストをレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使います。エディターを離れずに Copilot Chat の agent mode、MCP サーバー、カスタム エージェントを試します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
