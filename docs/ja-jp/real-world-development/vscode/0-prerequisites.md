---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の演習を始める前に、環境を準備します。Tailspin Toys リポジトリのコピーを作成し、作業用の [Codespace][codespaces] を起動して、統合開発環境 (IDE) で GitHub Copilot Chat が使えることを確認します。

## ラボ用リポジトリを設定する

ラボ用のリポジトリを作るには、[テンプレート リポジトリ][template-repository]から自分用のコピーを作成します。コピーには演習に必要なファイルが含まれます。

1. 新しいブラウザー ウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ラボ用リポジトリのページで **Use this template** を選択し、**Create a new repository** を選択します。

   ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントの一環として参加している場合は、メンターの指示に従います。それ以外の場合は、GitHub Copilot を利用できる Organization に新しいリポジトリを作成します。

   ![リポジトリ テンプレートの設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス (**organization-or-user-name/repository-name**) を控えます。演習中に参照します。

> [!NOTE]
> **バックログの準備は完了しています**
>
> テンプレートからリポジトリを作成すると、GitHub Issue のバックログも自動で作成されます。ワークショップではこの Issue を使うため、自分で作成する必要はありません。

## Codespace を作成する

次に、演習で使う Codespace を作成します。[GitHub Codespaces][codespaces] は、ブラウザーでコードを記述、実行、デバッグできるクラウド開発環境です。複数のプログラミング言語、拡張機能、ツールをサポートする IDE を利用できます。

1. 作成したリポジトリを開きます。
2. 緑色の **Code** ボタンを選択します。

   ![Code ボタンを選択する画面](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選択し、**+** ボタンを選択して Codespace を作成します。

   ![新しい Codespace を作成する画面](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかりますが、サービスを手動でインストールするよりも短時間で準備できます。その間に GitHub Copilot の機能を確認してもかまいません。

> [!CAUTION]
> 今後の演習で Codespace に戻ります。今はブラウザーのタブで開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの[開発コンテナー][dev-containers]で実行できます。どちらにも演習に必要な前提条件が含まれます。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、プロンプトが表示されたら **Reopen in Container** を選択します。Codespace と同じ開発コンテナーが構築されます。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## GitHub Copilot Chat と agent mode を使う

VS Code で GitHub Copilot Chat の agent mode を使うには、IDE に GitHub Copilot Chat 拡張機能が必要です。GitHub Codespace では通常、すでにインストールされています。

> [!TIP]
> 拡張機能がない場合は、[Visual Studio Code Marketplace から GitHub Copilot Chat をインストール][copilot-chat-extension]できます。または VS Code の Extensions ビューを開き、**GitHub Copilot Chat** を検索して **Install** を選択します。

拡張機能をインストールした後、GitHub アカウントで認証する必要がある場合があります。

1. Codespace に戻ります。
2. エディター右側に Copilot Chat が表示されていない場合は、Codespace 上部の **Copilot Chat** アイコンを選択します。
3. Copilot Chat に `Hello world` などのメッセージを入力して <kbd>Enter</kbd> を押し、Copilot Chat を起動します。
4. 未認証の場合は GitHub アカウントへのサインインが求められます。画面の指示に従って認証します。

   ![Copilot Chat の認証プロンプトの例](../../../_images/ex1-copilot-authentication.png)

5. 認証後、Copilot Chat が表示されることを確認します。

## まとめ

ラボ用リポジトリのコピーを作成し、コードを書くための Codespace の作成を開始しました。

## 次のステップ

次は Copilot に作業を依頼します。[演習 1 - カスタム指示][next-lesson]に進み、プロジェクトの規約を伝えます。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces のクイックスタート][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
