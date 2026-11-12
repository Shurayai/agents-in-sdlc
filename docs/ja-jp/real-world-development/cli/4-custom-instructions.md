---
title: "レッスン 4 - カスタム指示で Copilot をガイドする"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、フィルタリングのコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときは、コンテキストが重要です。作業方法に決まりがある場合、そのガイダンスを Copilot が参照できるようにします。[指示ファイル][instruction-files]には、求めるコードだけでなく、その構成方法も記述できます。フィルタリング機能を実装したので、Copilot が参照した指示を確認し、文書化の標準を追加して、コードに適用します。

このレッスンでは、次のことを行います。

- リポジトリの指示とパスで適用範囲を限定した指示がエージェントにどう使われるかを確認します。
- コーディング標準に従うよう指示ファイルを更新します。
- 指示ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には開発ガイドラインがあります。コメントはコードの言い換えではなく意図や自明でない判断を説明すること、`db/` と `src/lib/` のエクスポート関数は目的、パラメーター、戻り値を TSDoc/JSDoc で記述すること (該当する場合は注入可能な `db` 引数も含む)、再利用可能な Astro コンポーネントは `Props` の契約を文書化すること、関連コードが変わった際にはコメントを更新すること、既存の書式と lint のガイダンスを維持することが求められます。

## 指示ファイル

カスタム指示を使うと、コーディング スタイルや要件などのコンテキストを Copilot に伝えられます。リポジトリ全体に適用するものと、特定の種類のファイルやタスクに適用するものがあります。

- `.github/copilot-instructions.md` は、リポジトリへの**すべての** Copilot リクエストで使う単一の指示ファイルです。技術スタック、プロジェクトの概要、広く適用されるベスト プラクティスなどを記載します。
- `.github/instructions/*.instructions.md` は、TypeScript や Astro などの言語、UI コンポーネントや単体テストの作成など、特定のタスクやファイルの種類に指針を与えます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示と、`applyTo` フロントマターで適用範囲を指定した `*.instructions.md` ファイルを使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの形式の指示ファイルにも対応しています。詳細は[カスタム指示のサポート][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベスト プラクティス

このワークショップでは作成方法の全容は扱いませんが、サンプル プロジェクトには代表的な構成例があります。

- `copilot-instructions.md` には、構築中のもの、プロジェクトの構造、全体に適用するコーディング標準などを記載します。
- `*.instructions.md` には、単体テスト、Astro コンポーネント、データ層など、特定のファイルやタスクに関する指針を記載します。
- 自然な言葉で明確に書き、良い例と避けるべき例を示します。

指示ファイルの作成方法は 1 つではありません。プロジェクトやシナリオで試しながら調整してください。

> [!TIP]
> GitHub Copilot を使うプロジェクトでは、指示ファイルを整備してください。このプロジェクトには[ユーザー インターフェイス (UI) の指示][ui-instructions]や [Astro の指示][astro-instructions]などがあります。
>
> Copilot に指示ファイルの作成を手伝わせることもできます。たとえば VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` を使います。操作方法は各ハーネスの該当レッスンで説明します。
>
> テンプレートや出発点を探す場合は、指示ファイルやカスタム エージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 指示ファイルを確認する

スターター プロジェクトには指示ファイルが含まれています。変更前に内容を確認します。

1. Codespace に戻ります。
2. Codespaces エディターで `.github/copilot-instructions.md` を開きます (ターミナルではありません)。
3. プロジェクトの説明とコーディング ガイダンスを確認します。この指示はリポジトリ内の Copilot とのすべてのやりとりに適用されます。
4. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの指示を確認します。
5. `.github/instructions/unit-tests.instructions.md` を開き、適用対象のファイルを決める `applyTo` フィールドを確認します。
6. `.github/instructions/drizzle.instructions.md` のリンクを確認します。指示を小さく再利用可能なファイルに分け、プロジェクト内の例を示せます。

## チームのガイダンスに合わせて指示を更新する

新しく生成する TypeScript に TSDoc コメントを追加するよう、`.github/copilot-instructions.md` を更新します。

1. **Code formatting guidance** セクションを探します (35 行目付近)。
2. 最後の箇条書きに次の項目を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

変更は自動的に保存されます。

## 更新したガイダンスを適用する

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。指示を保存した後、フィルタリングの会話を再開し、機能のコンテキストを保ったまま新しい指示を読み込ませます。

1. フィルタリングの会話が開いている場合は `/exit` を入力します。Copilot CLI は会話を自動保存します。
2. リポジトリのルートで `game-filters-cli` ブランチにいることを確認し、保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   プロンプトが表示されたら、フィルタリングの会話を選択し、`game-filters-cli` ブランチがチェックアウトされていることを確認します。

3. Copilot に次のプロンプトを送信します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。TSDoc コメントが追加され、コードを正確に説明していることを確認します。

## まとめと次のステップ

このレッスンでは、次の作業を行いました。

- リポジトリの指示とパスで適用範囲を限定した指示がエージェントにどう使われるかを確認しました。
- コーディング標準に従うよう指示ファイルを更新しました。
- 指示ファイルがコードに与える影響を確認しました。

Copilot CLI が指示ファイルを利用する方法を確認し、機能に新しい標準を適用しました。次は[再利用可能な quality-checks スキルをカスタマイズして実行し][next-lesson]、lint とテストを一貫して実行します。

## リソース

- [Copilot CLI にカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けの優れたカスタム指示を書くための 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルなどのコレクション][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
