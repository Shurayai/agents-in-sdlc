---
title: "レッスン 9 - GitHub Copilot CLI の便利な機能"
description: "コンテキストやモデルの管理、セッション共有、並列作業、クラウドへの委任に使うコマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

GitHub Copilot CLI には、追加の機能や設定を利用するためのスラッシュ コマンドがあります。これまで使った `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` に加えて、コンテキスト、モデル、セッション共有、任意のクラウド委任に使うコマンドを確認します。

このレッスンでは、`/context` と `/compact` で会話コンテキストを調べ、`/model` で利用可能なモデルを確認し、`/share` によるセッションのエクスポートや共有を学びます。さらに、並列作業、worktree、cloud agent への委任に使える任意のコマンドも確認します。

## コンテキストを確認する

会話が長くなると、モデルのコンテキスト ウィンドウの上限に近づく場合があります。Copilot CLI は必要に応じて自動で会話を圧縮しますが、コマンドで状況を確認し、手動で圧縮することもできます。

1. Codespace に戻り、リポジトリのルートで Copilot CLI を起動します。
2. `/context` を入力します。
3. モデル、トークン使用量、システム指示、ツール、メッセージ、空き領域の内訳を確認します。
4. `/compact` を入力して会話を圧縮します。
5. 再度 `/context` を入力し、結果を比較します。会話が短い場合、大きな違いがないこともあります。

Copilot CLI はコンテキスト ウィンドウが埋まると自動で圧縮します。タイミングを選ぶ場合は `/compact` を使います。無関係なタスクに移るときは `/clear` または `/new` で新しい会話を開始します。

## モデルを選ぶ

`/model` を入力し、利用できるモデルと使用状況を確認します。現在のモデルを使い続けるか、別のモデルを選ぶか、<kbd>Esc</kbd> で一覧を閉じます。

## セッションを共有する

`/help` を入力し、インストール済みバージョンの `/share` オプションを確認します。セッションは Markdown または HTML ファイルにエクスポートしたり、共有リンクや GitHub gist を作成したりできます。共有する場合は、送信や公開の前に内容を確認してください。プロンプト、応答、プロジェクトの詳細が含まれることがあります。公開は任意です。チームが共有を意図していない情報を公開しないでください。

## 任意: 並列作業と委任

コア ワークショップを完了した後、より大きな作業には次のコマンドを試せます。

- `/fleet` は独立したサブタスクをサブエージェントに分け、並列実行できます。
- `/worktree` は別のタスク用に独立した Git worktree を作成できます。
- `/delegate` はタスクを Copilot cloud agent に送り、非同期に作業させます。プルリクエストが作成される場合があります。

これらの操作では worktree やリモート作業が追加される場合があります。新しい作業から始め、通常の手順で結果をレビューしてください。非同期エージェントについては、[cloud agent ワークショップ][cloud-workshop]を参照してください。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- `/context` と `/compact` で Copilot のコンテキスト管理を確認しました。
- `/model` で利用可能なモデルを確認しました。
- `/share` でセッションをエクスポートまたは共有する方法を確認しました。
- 並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認しました。

スラッシュ コマンドで Copilot CLI の設定、セッション共有、内部状態の確認を行いました。次は[学んだ内容を振り返り][next-lesson]、さらに学ぶための手順を確認します。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
