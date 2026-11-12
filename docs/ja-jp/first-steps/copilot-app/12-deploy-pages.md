---
title: "レッスン 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot app を使って Pages ワークフローを設定し、プルリクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

GitHub Pages で Space Quiz をデプロイし、誰でもアクセスできるようにします。Copilot はワークフローの準備とデプロイを支援しますが、変更をレビューし、サイトが公開されたことを確認するのは開発者です。

このレッスンでは、次のことを行います。

- Copilot に GitHub Pages の設定を依頼します。
- マージ前にワークフローとプルリクエストをレビューします。
- デプロイの状況を追跡し、公開されたサイトを確認します。

## シナリオ

Space Quiz はすでに GitHub リポジトリにありますが、まだ簡単に試せる場所がありません。GitHub Pages で単一ファイルのサイトを公開すると、サーバーやランタイム依存関係を追加せずに公開 URL からアクセスできるようになります。

## Copilot にサイトのデプロイを依頼する

`space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

```plaintext
Enable GitHub Pages for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and merge it after required checks pass. Monitor the deployment until it succeeds, then report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![3段階の図: マージ済みの space-quiz プルリクエスト、Build website、Upload artifact、Deploy to Pages の各ステップが成功した GitHub Actions の Deploy website 実行、yourname.github.io/space-quiz/ で公開された Space Quiz。](../../../_images/first-steps-app-pages-deploy.svg)

> [!WARNING]
> このプロンプトは、プルリクエストの作成とマージ、およびリポジトリの Pages 設定の変更をエージェントに依頼します。続行する前に、差分、デプロイ権限、GitHub の承認要求を確認してください。

## ワークフローをレビューしてデプロイを確認する

次の手順で、変更を確認して公開サイトが利用できることを確かめます。

1. README が、リポジトリにまだ存在しない場合にのみ追加されていることを確認します。
2. ビルドとデプロイの手順を含め、プルリクエストの変更をレビューします。
3. 必須のプルリクエストチェックが成功した後にのみマージします。
4. GitHub Actions のデプロイ実行が成功するまで確認します。
5. 報告された URL を開き、Space Quiz が読み込まれることを確認します。

エージェントが Pages を有効にできない場合やプルリクエストをマージできない場合は、エージェントが示す具体的な手順に従います。デプロイが成功し、公開サイトが読み込まれるまでは完了とみなさないでください。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- Copilot に GitHub Pages のデプロイを設定するよう依頼しました。
- マージ前にワークフローとプルリクエストをレビューしました。
- デプロイを追跡し、公開されたサイトを確認しました。

Space Quiz を公開し、エージェントの報告だけに頼らずデプロイを確認しました。続けて[レッスン 13: レビューと次のステップ][next-lesson]に進みます。

[next-lesson]: ../13-review/
