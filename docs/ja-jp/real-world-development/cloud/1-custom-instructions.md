---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときはコンテキストが重要です。作業方法や Copilot が知るべき背景情報がある場合、その情報にアクセスできるようにします。[指示ファイル][instruction-files]を使うと、Copilot に何を実行するかだけでなく、どのように実行するかも伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパスで適用範囲を限定した指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot にどう伝わるかを確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code や CLI のハーネスとは異なり、ここでは変更前後のプロンプトを比較しません。Copilot cloud agent は GitHub Issue 上で非同期に動作するため、リアルタイムの比較が難しいからです。後の演習で cloud agent が作成するプルリクエストをレビューするときに、指示ファイルの影響を確認します。

## 指示ファイル

### シナリオ

Tailspin Toys には開発ガイドラインがあります。

- データ層には必ず単体テストを用意します。
- UI はダーク モードで、現代的な見た目にします。
- コードのドキュメントには TSDoc コメントを使います。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを追加します。

指示ファイルを使い、Copilot がこれらの開発慣行に沿って作業できるようにします。

### カスタム指示

カスタム指示は、コーディング スタイルや要件などのコンテキストを Copilot に伝えます。リポジトリ全体、または特定の種類のファイルに適用する指示を作成できます。

- `.github/copilot-instructions.md` は、リポジトリに対する**すべての** Copilot リクエストで使われる単一の指示ファイルです。技術スタック、プロジェクトの概要、ベスト プラクティスなど、広く適用される情報を記載します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイルの種類に指針を与えるファイルです。TypeScript や Astro などの言語、UI コンポーネントの作成、単体テストの追加などに利用できます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示と、`applyTo` フロントマターで適用範囲を指定した `*.instructions.md` ファイルを使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの形式の指示ファイルにも対応しています。詳細は[カスタム指示のサポート][custom-instructions-support]を参照してください。

### 指示ファイルを管理するためのベスト プラクティス

この演習では作成方法の全容は扱いませんが、サンプル プロジェクトには代表的な構成例があります。

- `copilot-instructions.md` には、構築中のもの、プロジェクトの構造、全体に適用するコーディング標準などを記載します。
- `*.instructions.md` には、単体テスト、Astro コンポーネント、データ層など、特定のファイルやタスクに関する指針を記載します。
- 自然な言葉で明確に書き、良い例と避けるべき例を示します。

指示ファイルの作成方法は 1 つではありません。プロジェクトやシナリオで試しながら調整してください。

> [!TIP]
> GitHub Copilot を使うプロジェクトでは、指示ファイルを整備してください。このプロジェクトには [UI の指示][ui-instructions]や [Astro の指示][astro-instructions]などがあります。
>
> Copilot に指示ファイルの作成を手伝わせることもできます。たとえば VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` を使います。操作方法は各ハーネスの該当レッスンで説明します。
>
> テンプレートや出発点を探す場合は、指示ファイル、カスタム エージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

プロジェクトに含まれる指示ファイルを読み、Copilot に渡されるコンテキストを確認します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡単な説明と **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** 内の **GitHub Actions Workflows** の指針も、Copilot とのすべてのやりとりに適用されます。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの指示ファイルを確認します。
4. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドを確認します。これはリポジトリのルートからの glob で、たとえば `**/*.test.ts` に一致する TypeScript テスト ファイルに指示が適用されます。
5. 単体テスト作成に関する指示を確認します。
6. `.github/instructions/drizzle.instructions.md` の末尾に移動し、`unit-tests.instructions.md` などの指示ファイルや既存ファイルへのリンクを確認します。大きな指示を再利用可能な小さなファイルに分け、例を参照できます。ここにあるパスはリポジトリのルートではなく、指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはコーディング標準が記載されていますが、コード内のドキュメントはまだ必須ではありません。次の手順で TSDoc コメントとファイル先頭のコメントを追加します。

## リポジトリ全体に適用する標準を追加する

ドキュメントをコード内に記述する標準を加えます。まずブランチを作成します。cloud agent は Issue の対象ブランチから作業を開始しますが、ここでは変更を整理してコミットします。

1. Codespace のターミナルで新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. `.github/copilot-instructions.md` を開き直します。
3. 27 行目付近にある **Code formatting requirements** セクションを探します。既存の標準にコード内のドキュメントの規則がまだないことを確認します。
4. 既存の標準の直後に、次の Markdown を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. `copilot-instructions.md` を保存します。

> [!TIP]
> リポジトリ全体に適用する標準は `.github/copilot-instructions.md` に、言語やファイルの種類、タスクに特化した指示は `*.instructions.md` に追加します。ここで加えたドキュメント規則はプロジェクト全体の標準なので、リポジトリ レベルのファイルが適しています。

## 指示の変更をコミット、プッシュ、マージする

次の演習で Issue を Copilot に割り当てると、cloud agent は `main` からブランチを作成します。追加した指示を使えるように、変更を `main` にマージします。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプルリクエストを開き、マージします。次の演習で Issue を割り当てるとき、cloud agent はこの指示を読み込みます。

> [!TIP]
> このワークショップで `main` に直接作業する場合は、ブランチの作成を省略して `main` にコミットしてもかまいません。ここでは実際のプロジェクトでの手順に近づけるためにブランチを使います。

## まとめと次のステップ

この演習では、次のことを行いました。

- リポジトリのカスタム指示とパスで適用範囲を限定した指示ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot にどう伝わるかを確認しました。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。

このプロジェクトの指示ファイルから Copilot がコンテキストを得る方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。残りのハーネスで cloud agent が作成するプルリクエストをレビューするときに、この標準の影響を確認します。

次は[最初の Issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 向けの優れたカスタム指示を書くための 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルなどのコレクション][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
