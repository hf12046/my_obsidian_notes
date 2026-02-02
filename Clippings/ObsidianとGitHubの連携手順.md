---
title: ObsidianとGitHubの連携手順
source: https://zenn.dev/ofurousagi/articles/250801_obsidian-github-sync
published: 2025-08-01
created: 2026-01-20
description:
tags:
  - clippings
  - github
  - obsidian
---
[[スマホのObsidianをGitで同期(2024.11)]]
### 1\. Vault（保管庫）を作成

今回は `Valut/my-obsidian-notes` ディレクトリを作成しました。  
Valutディレクトリ直下に保管庫を置く必要は特にはありませんが、今後保管庫を増やしたい・分けたい場合のことを考えてこのようなファイル構成にしました。

```md
Valut
└─ my-obsidian-notes
```

この `my-obsidian-notes` はこのあとgithubのリポジトリ名として使用します。

### 2\. GitHubにリポジトリを作成

ここで設定したリポジトリ名と、ObsidianのVault名は一致している方が管理しやすいため、今回は `my-obsidian-notes` としました。

```md
https://github.com/username/my-obsidian-notes.git
```

### 3\. ローカルの保管庫ディレクトリをリポジトリ化

```bash
cd /Users/username/vault/my-obsidian-notes/
git init
git remote add origin https://github.com/username/obsidian-notes.git
```

### 4\. コミット&プッシュ

```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```

### 5\. コミュニティプラグインからGitをインストール

1. **`Setting > コミュニティプラグイン` を開く**
2. **「コミュニティプラグインを有効化」をクリックし、プラグインをインストールできるようにする**  
	![コミュニティプラグインを有効化](https://res.cloudinary.com/zenn/image/fetch/s--tzdnGMSu--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/ae818053a7a6773bad55aa47.png%3Fsha%3Df0e74269f38448140a70c88bec244b55ea680e81)
3. **`閲覧 > Git` を検索しインストール&有効化**  
	![閲覧](https://res.cloudinary.com/zenn/image/fetch/s--MGDQlb-k--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/3c57cbb954f22e456d513fa6.png%3Fsha%3Ddda731a0094d16386406bdd0744d36c4c45f499b)  
	![Git`を検索しインストール&有効化](https://res.cloudinary.com/zenn/image/fetch/s--kJ5KdbYR--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/cb315aea5fec03656f107798.png%3Fsha%3D767aab4b8db678407128cceab973ea8e66862dca)

### 6\. 自動コミット&プル、コミットメッセージの設定

1. **`setting > Gitプラグインの設定` を開く**
2. **自動コミット&プッシュの間隔を設定**
	- `Auto commit-and-sync interval(minutes)` に任意の数値を入力  
		デフォルトが0（自動でコミット&プッシュされない）になっているので、今回は10分ごとにコミット&プッシュされるように10と入力します。
3. **自動プルの間隔を設定**
	- `Auto pull interval(minutes)` に任意の数値を入力  
		デフォルトが0（自動でプルされない）になっているので、今回は10分ごとにプルされるように10と入力します。
4. **必要に応じてコミットメッセージを設定**  
	自動コミットと手動（マニュアル）コミットでコミットメッセージを変えることができます。  
	私は `auto commit` と `manual commit` でコミットメッセージを変えました。

![Auto pull interval(minutes)](https://res.cloudinary.com/zenn/image/fetch/s--d_rbuqVA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/850135d193cf4fd8dd3866e0.png%3Fsha%3Dbd1245d8d305de37e37496c29a4edc1fe83090fc)  
![Auto pull interval(minutes)](https://res.cloudinary.com/zenn/image/fetch/s--QbJxgTNv--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/c824c2db1343c32fd146b82f.png%3Fsha%3Da4e426327e6295fff04caad4d79cfe082fa20aa6)

他の項目は必要に応じて設定してください。

### 7\. パスを通す

1. **`which` でコマンドのパスを確認**

```bash
which git
/usr/local/bin/git
```

1. **Gitプラグインにパスを記載**  
	![Gitプラグインにパスを記載](https://res.cloudinary.com/zenn/image/fetch/s--JvfjIa3d--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_1200/https://storage.googleapis.com/zenn-user-upload/deployed-images/65bec777081d0a2df84d8376.png%3Fsha%3D6b562fe732966df9a1fc2d615f83e459e92d9622)
- ディレクトリを追加する必要があるため、 `/usr/local/bin/git` の `git` の部分は不要
- `/usr/bin` は保険として追加（なくてもOK）

### 8\. コミット&プッシュの確認

Obsidianからファイルを編集して、設定した間隔後にGitHubに反映されているか確認します。

これでObsidianとGitHubの連携が完了しました。