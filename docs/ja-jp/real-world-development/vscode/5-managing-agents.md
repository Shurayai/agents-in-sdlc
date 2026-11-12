---
title: "演習 5 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム エージェント][previous-lesson] |
|:--|

Agent mode の Copilot は、コードベースを調べ、変更を提案してファイルを編集し、コマンドを実行します。VS Code の Copilot Chat では、ツールの呼び出しやファイルの編集をリアルタイムで確認できます。差分をインラインでレビューし、個々の変更を採用または却下し、追加プロンプトで作業を調整できます。

この演習では、アクセシビリティ エージェントの作業をリアルタイムで監視し、提案された編集をレビューして採用し、進行中のセッションに高コントラスト モードとともにライト モードも追加するよう依頼します。

## シナリオ

[演習 4][previous-lesson]で使ったアクセシビリティ カスタム エージェントは、高コントラスト モードを実装しています。作業中、デザイン チームから、既定のテーマが暗すぎる利用者向けにライト モードも追加してほしいと依頼がありました。新しい会話を始めるのではなく、既存のセッションに指示を追加します。

## Copilot の進行状況を監視する

Copilot Chat ビューには、エージェントが調べたファイル、実行したコマンド、提案した編集が表示されます。編集は差分と **Keep** / **Undo** の操作とともにインラインで表示されます。

1. 演習 4 で使った Copilot Chat ビューに戻ります。
2. エージェントの作業中に Chat をスクロールし、ツールの呼び出しを確認します。ファイルの読み取りや編集、実行を求めるターミナル コマンドが表示されます。
3. ファイル編集の差分が表示されたら、**Keep** で変更を採用し、**Undo** で取り消して再試行させます。
4. Chat 上部の **Files changed** を開き、このセッションで変更されたファイル全体を確認します。

> [!NOTE]
> ターミナル コマンドの実行などに許可が必要な場合、エージェントは **Allow** を表示して一時停止します。内容を確認し、許可してよいコマンドだけを承認してください。

5. エージェントが高コントラスト モードの実装を終え、変更を要約するまで待ちます。

## ライト モードを追加するようエージェントに指示する

同じ会話を続けると、エージェントは変更済みのコンポーネント、スタイル、local storage のパターンを含むこれまでのコンテキストを保てます。

1. Copilot Chat の入力欄に次のプロンプトを送信します。

   ```plaintext
   Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
   ```

2. エージェントが既存の変更を調べ、ライト モードの追加を提案する様子を確認します。
3. 高コントラスト モードと同様に、追加された各編集をレビューし、**Keep** または **Undo** を選択します。
4. エージェントの方針が意図と異なる場合 (例: 切り替え UI を予期しない形でリファクタリングする場合) は、Chat 入力欄の横にある **Stop** で停止し、明確な追加プロンプトを送ります。

> [!TIP]
> 作業中のセッションに追加指示を送ると、最初からやり直すより速く方向を調整できます。たとえば「CSS を簡潔にして、セレクターの重複ではなく CSS 変数を使う」、「3 つ目の切り替えを追加せず、既存の設定パネルにライト モードを組み込む」、「両方の切り替えにキーボード ショートカットを追加する」と依頼できます。

## 作業セットをレビューする

コミット前にエージェントが変更したすべてのファイルを確認します。

1. VS Code で **Source Control** ビューを開きます。
2. Astro コンポーネント、スタイル、関連テストなど、変更ファイルの一覧を確認します。
3. 変更されたファイルをいくつか開き、差分を確認します。カスタム エージェントが示したアクセシビリティ パターン、Accessible Rich Internet Applications (ARIA) 属性、キーボード操作、セマンティック HTML、local storage による設定保持が反映されていることを確認します。
4. 問題がなければ **Source Control** パネルで変更をステージしてコミットします。次のレッスンで公開します。

## まとめと次のステップ

Copilot Chat の agent mode で進行中のセッションを監視して方向を調整しました。ファイル編集を確認し、個別の変更を採用または却下し、コンテキストを保ったまま追加プロンプトを送りました。

このレッスンでは、エージェントの作業をリアルタイムで監視し、個々の編集を採用または却下し、追加プロンプトでセッションの方向を変更しました。次は[アクセシビリティ作業をプルリクエストとして公開し][next-lesson]、ラボ全体でローカル カスタム エージェントが作成した変更をレビューします。

## リソース

- [VS Code の Copilot Chat][copilot-chat-vscode]
- [Agent mode の使用][agent-mode]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
