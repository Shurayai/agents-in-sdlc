---
title: "演習 5: GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

このラボでは、ユーザー体験と機能を改善する複数のタスクを GitHub Copilot に依頼しました。コードへのドキュメント追加、関連ゲーム機能、高コントラストとライト モードを含むアクセシビリティ機能を確認し、必要であれば Copilot に改善を依頼します。

### シナリオ

生成 AI を利用してもソフトウェア設計と DevOps の基本は変わりません。生成コードをレビューし、通常の DevOps プロセスを行います。チーム全体でレビューを有効にする前に、ドキュメント、関連ゲーム、アクセシビリティ機能に関する Copilot の提案を確認します。

## GitHub Copilot cloud agent のセキュリティ

cloud agent は非同期に、監督なしで作業するため、安全性を保つ制約があります。

- Copilot はリポジトリに対する読み取りアクセスと、コード用ブランチに対する書き込みアクセスのみを持ちます。
- cloud agent は GitHub Actions 内に一時的な環境を作成して実行されます。
- GitHub Actions ワークフローの実行には、人間の承認が必要です。
- Model Context Protocol (MCP) サーバーを含む外部リソースへのアクセスは、既定で制限されています。[cloud agent のファイアウォール][agent-firewall]を参照してください。

## 生成されたドキュメントをレビューする

まず、GitHub Copilot cloud agent がコード ドキュメントを追加した最初のプルリクエスト (PR) を GitHub.com で確認します。

> [!NOTE]
> PR に Copilot がファイアウォールでブロックされたという警告が表示される場合があります。外部リソース (外部 MCP サーバーへの呼び出しを含む) へのアクセスは既定で制限されているため、これは想定された動作です。必要であれば[cloud agent のファイアウォールを構成または無効化][agent-firewall]できます。

1. github.com のリポジトリに戻ります。
2. **Pull Requests** を選択します。
3. **Add missing documentation** などのタイトルの PR を開きます。

> [!NOTE]
> Copilot が作業中の場合、PR のタイトルに **[WIP]** が含まれます。完了するまで待ちます。数分かかる場合があります。

4. PR が準備できたら **Files changed** タブを選択し、変更を確認します。

   ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. TSDoc コメントやその他のドキュメントが追加されたコードを確認します。変更内容は状況によって異なります。Exercise 2 で確認した指示ファイルによる TSDoc コメント、TypeScript 規約、ファイル ヘッダーがあるかを確認します。
6. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローの承認待ちを示すインジケーターがあるか確認します。
8. 承認待ちの場合は **Approve and run workflows** を選択します。

   ![Approve and run workflows ボタン](../../../_images/shared-approve-workflows.png)

9. PR のチェック欄でワークフローがキューに入り、単一 Astro アプリのプロジェクト チェックが成功することを確認します。数分かかる場合があります。

## GitHub Copilot に変更を依頼する

PR やコードのインライン コメントで、チーム メンバーにするように Copilot にメンションして変更を依頼できます。Copilot はコメントを受け取り、別のセッションを開始します。結果は一定ではないため、依頼内容を一律に指定することはできません。たとえば、コード ファイルの先頭に説明コメントを追加する、TypeScript と Astro ファイルに TSDoc コメントを追加する、Astro アプリの構造を説明する README を作る、といった改善を依頼できます。

1. PR またはコードのインライン コメントで **@copilot** をメンションし、生成されたドキュメントへの変更を依頼します。上記の例でも、別の要望でもかまいません。
2. **View Session** を選択し、Copilot が変更する様子を確認します。更新のために新しいセッションが始まります。
3. **Back to pull request** を選択して PR に戻ります。

   ![プルリクエストに戻るボタン](../../../_images/ex7-back-to-pr.png)

4. Copilot が作業を完了した後、新しいコミットが PR に追加されたことを確認します。
5. **Files changed** タブで変更をレビューします。

満足するまで改善を繰り返せます。準備ができたら、ドラフト PR をレビュー可能な状態にして `main` にマージします。

![PR をレビュー可能な状態にする操作](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する Issue に対し、Copilot が作成した PR を確認します。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Show related games on the game details page** などのタイトルの PR を選択します。
4. **Files changed** タブを選択して、生成されたコードをレビューします。
5. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
6. ワークフローの承認待ちインジケーターがあることを確認します。
7. 承認待ちの場合は **Approve and run workflows** を選択します。

   ![Approve and run workflows ボタン](../../../_images/shared-approve-workflows.png)

8. PR のチェック欄でワークフローがキューに入り、単一 Astro アプリのチェックが成功することを確認します。数分かかる場合があります。
9. **任意:** 関連ゲーム機能を手動でテストするには、Codespace で Copilot が作成したブランチに切り替えます。`<branch-name>` を実際のブランチ名 (例: **copilot/fix-8**) に置き換えて、次のコマンドを実行します。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

関連ゲーム機能が実装されました。PR の **Conversation** タブにコメントを追加すると、表示するゲーム数や、指示の変更前に割り当てたため不足しているファイル ヘッダーや TSDoc コメントなどを調整するよう Copilot に依頼できます。

## アクセシビリティ機能をレビューする

最後に、アクセシビリティ カスタム エージェントが実装した機能をレビューします。この PR には、Exercise 3 で依頼した高コントラスト モードと、Exercise 4 で追加依頼したライト モードの両方が含まれます。

1. GitHub.com のリポジトリに戻ります。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** などのタイトルの PR を選択します。

> [!NOTE]
> Copilot が作業中の場合、PR に **[WIP]** が含まれます。作業が完了するまで待ちます。

4. **Files changed** タブを選択し、生成コードをレビューします。
5. 特に次の点を確認します。
   - モード切り替え用のユーザー インターフェイス (UI) コンポーネント
   - 利用者の設定を保存する local storage
   - 高コントラスト モードとライト モードのカスケーディング スタイル シート (CSS) またはスタイル変更
   - アクセシビリティ属性 (Accessible Rich Internet Applications (ARIA) ラベル、キーボード操作など)
   - モード切り替えを管理する JavaScript/TypeScript
6. 問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローの承認待ちインジケーターがあることを確認します。
8. 承認待ちの場合は **Approve and run workflows** を選択します。

   ![Approve and run workflows ボタン](../../../_images/shared-approve-workflows.png)

9. PR のチェック欄でワークフローがキューに入り、単一 Astro アプリのチェックが成功することを確認します。数分かかる場合があります。
10. **任意:** Codespace で Copilot が作成したブランチに切り替え、アクセシビリティ機能を手動でテストします。`<branch-name>` を実際のブランチ名に置き換えます。

   ```bash
   git fetch origin
   git checkout <branch-name>
   ```

   アプリを起動し、ブラウザーで高コントラスト モードとライト モードを切り替えます。ページを再読み込みしても設定が保持されることを確認します。

アクセシビリティ カスタム エージェントが、アクセシビリティのベスト プラクティスに沿うよう Copilot をガイドしたことを確認します。懸念や改善点があれば、前の PR と同様にコメントで **@copilot** に更新を依頼できます。

## 任意の演習 — 委任を続ける

cloud agent に実際のバックログ作業を任せると、その間に別の作業を進められます。習慣にするため、リポジトリに Issue を追加して Copilot に割り当てます。たとえば次の作業があります。

- ゲーム詳細ページに支援者向け問い合わせフォームを作る。
- ゲーム一覧ページにページネーションを実装する。
- データアクセス ヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent ハーネスを完了しました。

- リポジトリに含まれるカスタム指示を確認し、cloud agent の出力への影響を確認しました。
- Issue を Copilot cloud agent に割り当て、環境設定、計画、非同期の実行を確認しました。
- アクセシビリティ用カスタム エージェントを作成して使い、高コントラストとライト モードを追加しました。
- Copilot エージェント ページを Mission Control として使い、進行中のアクセシビリティ セッションを監視して方向を調整しました。
- Copilot が作成した PR をレビューして反復し、**@copilot** に変更を依頼し、ワークフローを承認しました。

## レビューと次のステップ

Cloud agent ハーネスを完了しました。ほかのハーネスで、今回の作業を別の環境でも試せます。

- 🖥️ **[VS Code ハーネス](../../vscode/)** — 統合開発環境 (IDE) で Copilot Chat の agent mode と MCP 統合を試します。
- 💻 **[CLI ハーネス](../../cli/)** — Plan、Autopilot、エージェント スキル、QA カスタム エージェント、Playwright MCP、Agent Merge、任意の `/delegate` による cloud agent への連携を使い、レビュー済みの 2 つの変更をターミナルからリリースします。

自分のリポジトリでは、次の作業も試してください。

- リファクタリングやテスト カバレッジの Issue を cloud agent に割り当てます。
- 別の分野のカスタム エージェントを作成します。
- 別の技術スタック用に `copilot-setup-steps.yml` を設定します。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot エージェントについて][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]
- [Copilot cloud agent のファイアウォールを構成する][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
