---
source: https://qiita.com/yuchi0999/items/477a47dffec98a1611b1
published: 2025-11-08
created: 2026-02-05
tags:
  - clippings
  - git
  - program
---
![](https://relay-dsp.ad-m.asia/dmp/sync/bizmatrix?pid=c3ed207b574cf11376&d=x18o8hduaj&uid=)

## 【GitHub×VsCode】基本操作まとめ

## はじめに

この記事では、開発に必須の **GitHub** と人気エディタ **VS Code** を連携させる方法を解説します。
まず、Git・GitHubを使う上で欠かせない **基本的な用語** を解説し、その上でVS Codeを用いた具体的な操作手順を紹介します。

## 💡 1. Git/GitHubの基本用語を理解する

GitとGitHubで使われる重要な用語を理解しておきましょう。

| 用語                     | 読み方                                    | 意味                                                                                                           |
| ---------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| **リポジトリ**              | Repository                             | プロジェクトのファイルと、その **全ての変更履歴** を保存する場所（ **倉庫** ）。   ローカルPC上のものを **ローカルリポジトリ** 、GitHub上のものを **リモートリポジトリ** と呼びます。 |
| **コミット**               | Commit                                 | ファイルの変更を履歴として **記録・確定** する作業。いわば「 **セーブ** 」です。                                                               |
| **ステージング**             | Staging                                | 変更したファイルをコミット対象として **一時的に準備する** 作業。コミットする変更を選ぶために使います。                                                       |
| **ブランチ**               | Branch                                 | 開発を並行して行うための **作業の分岐** 。メインの開発（通常は `main` など）に影響を与えずに新機能開発などを行うときに使います。                                      |
| **プッシュ**               | Push                                   | ローカルリポジトリでコミットした履歴を、 **リモートリポジトリ（GitHub）に送り出す** 作業。                                                          |
| **プル**                 | Pull                                   | リモートリポジトリ（GitHub）の最新の変更履歴を、 **ローカルリポジトリに取り込む** 作業。                                                           |
| **フェッチ**               | Fetch                                  | リモートリポジトリの最新情報を **ローカルに取得** するが、 **ローカルの作業ファイルは更新しない** 作業。Pullと違い、ローカルの変更に影響を与えません。                          |
| **マージ**                | Merge                                  | 分岐したブランチの変更内容を、 **別のブランチに合流させる** 作業。                                                                         |
| **プルリクエスト / マージリクエスト** | Pull Request (PR) / Merge Request (MR) | ブランチのマージを提案し、 **レビューを依頼する** ための機能。（ **PR** はGitHub、 **MR** はGitLabなどで使われる用語です。）                              |

## 💻 2. 事前準備

### 2-1. 必要なもの（インストール・アカウント作成）

- **VS Code** （高機能なコードエディタ）： [Visual Studio Code公式](https://code.visualstudio.com/) からダウンロード
- **Git** （バージョン管理システム）： [Git公式サイト](https://git-scm.com/install/windowsPC) からダウンロード
- **GitHubアカウント** （リモートリポジトリ）： [GitHub公式サイト](https://github.co.jp/) でアカウント作成

### 2-2. VS CodeとGitHubの連携（初期設定）

1. VS Codeの 「ソース管理」 ビュー（三つ又のアイコン）を開きます。
2. 初回利用時、「GitHubへのサインイン」が求められたら、指示に従って認証を完了させます。

---

## ⚙️ 3. VS Codeで実践する開発ワークフロー

### 3-1. リポジトリのクローン

既存のGitHubリポジトリをローカルPCにコピーする（ **クローン** ）操作をVS Codeで行います。

1. コマンドパレット (`Ctrl+Shift+P` または `Cmd+Shift+P`) を開きます。
2. 「 **Git: Clone** 」と入力し、選択。  
	[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/8959e078-a3aa-48b5-97e9-6a3ca476f30a.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2F8959e078-a3aa-48b5-97e9-6a3ca476f30a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1e264cbc2141b206abbe162532caba8b)
3. クローンしたいGitHubリポジトリのURLを入力（またはGitHubから選択）。  
	[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/d1c23df5-6dbc-45ff-8596-266408883673.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2Fd1c23df5-6dbc-45ff-8596-266408883673.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=e72a7f762877972c8385502d353ebf6a)
4. ファイルを保存するローカルフォルダを選択。
5. クローン完了。  
	[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/8f5073de-c50d-4d56-a2cd-f134a660d138.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2F8f5073de-c50d-4d56-a2cd-f134a660d138.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7c6e53bcf53cd4f62aa03d5889256c89)

### 3-2. ステージングとコミット（変更内容をローカルリポジトリに反映）

ファイルの変更は、VS Codeの「ソース管理」タブで管理します。  
（今回はREADME.mdの変更があったと仮定します。）  
[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/dea87f3c-0a45-4124-91d7-c5cb1cbbc98f.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2Fdea87f3c-0a45-4124-91d7-c5cb1cbbc98f.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7121da13f54b4eee8b69496ae8d6e873)

1. **ステージング**: 変更ファイルの横にある「＋」ボタンをクリックし、ステージングします。  
	※ステージングする際に変更箇所を確認すること  
	[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/5f4b3904-fedb-4a0b-a2b2-9c30d076b0a8.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2F5f4b3904-fedb-4a0b-a2b2-9c30d076b0a8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5c12f648994360fcf5345e22c4b5dfa1)
2. **コミット**: 上部にあるテキストボックスに **コミットメッセージ** を入力し、チェックマークのコミットボタンを押して履歴を記録（ **コミット** ）します。  
	※「 **コミットしてプッシュ** 」でローカルリポジトリに変更内容を反映＆リモートリポジトリにローカルリポジトリの変更内容の反映を一括で行うことも可能。  
	[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/5978309b-d072-4494-8c10-d5eb720be899.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2F5978309b-d072-4494-8c10-d5eb720be899.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=72fc0d9ce99b53f421c9a1621f2c0259)

### 3-3. GitHubへの反映（PushとPull）

| 操作 | 目的 | VS Codeでの操作 |
| --- | --- | --- |
| **Push** (送り出す) | ローカルのコミットをGitHubにアップロード | ソース管理ビューの「プッシュ」ボタン、または画面右下の雲のアイコン（⬆️）をクリック。 |
| **Pull** (取り込む) | GitHubの最新の変更をローカルに取り込む | ソース管理ビューの「プル」ボタン、または画面右下の同期アイコン（🔄）をクリック。 |

[![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/4038415/55cba749-4180-4bc4-adf5-33a8d43a6d4a.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F4038415%2F55cba749-4180-4bc4-adf5-33a8d43a6d4a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=130a264a389e87e722c48eb64c535cf3)

---

## 🤝 4. 共同開発への応用（ブランチとマージ）

### 4-1. ブランチの作成と切り替え

画面下部のステータスバー（通常は `main` と表示されている箇所）をクリックすると、 **ブランチの作成** や **切り替え** が簡単に行えます。

### 4-2. プルリクエストとマージ (Pull Request)

開発が完了したら、メインブランチへ合流（ **マージ** ）するために\*\*Pull Request (PR)\*\*を作成します。

1. VS Codeの拡張機能（例：GitHub Pull Requests and Issues）などを使ってPRを作成します。
2. PRがレビューされ、承認されると、変更がメインブランチに\*\*合流（マージ）\*\*されます。

---

## ✨ まとめ

Gitの基本用語を理解し、 **VS Codeのソース管理ビュー** を使うことで、Gitコマンドを覚えることなく、GitHubを活用した効率的な開発が行えます。

まずはこの記事を参考に、 **クローン → コミット → プッシュ** の一連の流れをVS Codeでマスターしましょう！

### 関連リンク

- [Git公式サイト](https://git-scm.com/)
- [GitHub 公式サイト](https://github.com/)
- [Visual Studio Code 公式サイト](https://code.visualstudio.com/)