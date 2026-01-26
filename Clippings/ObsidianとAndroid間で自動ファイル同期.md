---
title: ObsidianとAndroid間で自動ファイル同期
source: https://qiita.com/Marusankaku_E/items/ff01a0aaa198d9ec21bf
author:
published: 2025-11-25
created: 2026-01-14
description: はじめに こんにちは。エンジニアのまるさんかくです。 最近、Obsidianというメモアプリにハマっており、日記を書いたり、情報整理に使用しています。 Obsidianは「Markdownで素早く書ける」「リンクで関連づけができる」「プラグインで自由に拡張できる」といった...
tags:
  - clippings
---
![](https://relay-dsp.ad-m.asia/dmp/sync/bizmatrix?pid=c3ed207b574cf11376&d=x18o8hduaj&uid=)

## Qiitaにログインして、便利な機能を使ってみませんか？

あなたにマッチした記事をお届けします

便利な情報をあとから読み返せます

[ログイン](https://qiita.com/login?callback_action=login_or_signup&redirect_to=%2FMarusankaku_E%2Fitems%2Fff01a0aaa198d9ec21bf&realm=qiita) [新規登録](https://qiita.com/signup?callback_action=login_or_signup&redirect_to=%2FMarusankaku_E%2Fitems%2Fff01a0aaa198d9ec21bf&realm=qiita)

[@Marusankaku\_E](https://qiita.com/Marusankaku_E)

## ObsidianとAndroid間で自動ファイル同期

投稿日

## はじめに

こんにちは。エンジニアのまるさんかくです。  
最近、Obsidianというメモアプリにハマっており、日記を書いたり、情報整理に使用しています。  
Obsidianは「Markdownで素早く書ける」「リンクで関連づけができる」「プラグインで自由に拡張できる」といった特徴があり、使えば使うほど自分の知識ベースが育っていく感覚がとても気持ちいいアプリです。  
AndroidでもPCと同期する方法を探していたところ、Syncthingという方法が無料で、主流だということを知りました。  
この記事では、その導入手順をまとめていこうと思います。

### 前提条件

- PCでObsidianのセットアップが完了しており、Vaultが存在すること
- PCとAndroidが同じWi-Fiネットワークに接続できること（初回設定時）

### この方法のメリット

- **クラウド不要**: データがクラウドに保存されないためプライバシー面で優れている
- **高速同期**: 同一Wi-Fi内では超高速で同期
- **外出先からも同期可能**: インターネット経由でも同期可能
- **競合が少ない**: ファイル編集検出が正確で衝突が極めて少ない
- **無料**: 完全無料で制限なし

## セットアップ手順

### 1\. PC側のセットアップ

#### (1) Syncthingをインストール

1. [https://syncthing.net/](https://syncthing.net/) にアクセス
2. 「Download」をクリック  
	[![Pasted image 20251120070217.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/85b08548-4026-441b-8b85-02e87af055c7.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F85b08548-4026-441b-8b85-02e87af055c7.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=17837e541ad41a27ead8f56a0b0e9c3b)
3. 自分のOS（Windows/Mac/Linux）に合わせてインストーラを選択  
	[![Pasted image 20251120070402.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/859c3861-f1ce-48d4-b02d-fb1b90fc09b3.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F859c3861-f1ce-48d4-b02d-fb1b90fc09b3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=45cbf58a78f60fd342b7309eecf70d9e)
4. githubリポジトリに飛ぶので、Releaseからsetup.exeをダウンロード  
	[![Pasted image 20251120070326.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/701c112a-1e51-4c5b-b2f9-f382682f7c6a.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F701c112a-1e51-4c5b-b2f9-f382682f7c6a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=56ada4fbea2f127022067f986cab6e6f)  
	[![Pasted image 20251119075406.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/b45a01ab-6d17-418f-a061-955202e1d2db.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Fb45a01ab-6d17-418f-a061-955202e1d2db.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=75fd777e4c990e384d3f3674b112a78c)
5. インストーラーを実行してインストール

#### (2) 初回起動

1. Syncthingを起動すると、自動的にブラウザでWeb UIが開く
2. 通常は `http://127.0.0.1:8384` でアクセスできる
3. PCはこのWeb UIからすべての設定を行う  
	[![Pasted image 20251119075549.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/075596c4-655c-4f51-ac86-263ce8ed5a3b.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F075596c4-655c-4f51-ac86-263ce8ed5a3b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=95ced7929b2cf25e03c8b3ba85674b47)

### 2\. Android側のセットアップ

#### (1) Syncthing-Forkをインストール

**F-Droid版を推奨** （Google Play版よりバックグラウンド維持が安定）

1. **F-Droidアプリのインストール** （未インストールの場合）
	- ブラウザで「F-Droid」と検索
	- F-Droid公式サイトからAPKファイルをダウンロード
	- ダウンロードしたAPKファイルをタップしてインストール
	- 「不明なソースからのアプリを許可」する必要がある場合がある  
		[![Pasted image 20251120070714.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/c437d692-1f76-421c-8c40-37dce06510e4.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Fc437d692-1f76-421c-8c40-37dce06510e4.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a7666f53be3825602c60406e24bf9156)
2. **Syncthing-Forkのインストール**
	- F-Droidアプリを開く
	- 「Syncthing-Fork」で検索
	- インストール  
		[![Pasted image 20251120071027.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/d59779f2-bd1e-4ef2-b8ea-8e05b25a45ed.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Fd59779f2-bd1e-4ef2-b8ea-8e05b25a45ed.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=cf04244ccb8e2fd5af13ac5b03599e5e)

#### (2) 初回起動時の設定

1. **バッテリー最適化を無視する（必須）**
	- アプリ設定 → バッテリー最適化 → Syncthing-Fork → 「最適化しない」を選択
	- これを行わないと、バックグラウンドで同期が停止する可能性がある
2. **外部ストレージアクセスを許可する**
	- 初回起動時に表示される権限リクエストで「許可」を選択

### 3\. デバイス同士を接続する

#### QRコードで接続

1. **PC側でQRコードを表示**
	- Syncthing Web UIを開く（通常は `http://127.0.0.1:8384` ）
	- 右上の「メニュー」アイコン（歯車マーク）をクリック
	- 「IDを表示」をクリック
	- 自分のデバイス名と **デバイスID** （長い英数字の文字列）が表示される
	- QRコードが表示される
	[![Pasted image 20251120071255.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/962437d0-6c14-4acb-993f-d31ecc656e40.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F962437d0-6c14-4acb-993f-d31ecc656e40.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a35ee12a157aa9c656ed53056158f339)
2. **Android側でQRコードをスキャン**
	- Syncthing-Forkアプリを開く
	- 「デバイス」タブを開く
	- 右上の「+」ボタンをタップ  
		[![Pasted image 20251120071622.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/d3c483fa-0148-419e-90c1-5eb51ac4e284.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Fd3c483fa-0148-419e-90c1-5eb51ac4e284.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0acd03f79939a9a20ea44339588ad93e)
	- 「ID」のQRコードマークをタップ
	- PC画面のQRコードをスキャン
	- デバイス名を入力して「追加」をタップ
3. **接続状態の確認**
	- **PC側**: Web UIの「接続先デバイス」で接続状態を確認（緑色の丸で表示される）  
		[![Pasted image 20251120071834.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/19283028-9655-4d3a-a43c-c108465c089a.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F19283028-9655-4d3a-a43c-c108465c089a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=450089d789f2b9ab4d11482bb7cd6a56)
	- **Android側**: アプリの「デバイス」画面で接続状態を確認  
		[![Pasted image 20251120071933.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/b396070c-fb02-4bdb-9239-de3095616408.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Fb396070c-fb02-4bdb-9239-de3095616408.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2e054b2c736ef8c8e338798f4d62ddc8)

### 4\. Vaultフォルダの共有設定

#### (1) PC側でフォルダを追加

1. **フォルダを追加**
	- Syncthing Web UI → 「フォルダ」→ 「フォルダを追加」
2. **フォルダの設定**
	- **フォルダー名**: 任意の名前（例: "Obsidian"）
	- **フォルダパス**: Obsidian Vaultのフォルダを指定
		- Windows例: `C:\Users\あなた\Documents\ObsidianVault`
		- Mac例: `/Users/あなた/Documents/ObsidianVault`  
			[![Pasted image 20251120065059.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/f33335d8-1981-4b4b-8e44-af8bff74fad3.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Ff33335d8-1981-4b4b-8e44-af8bff74fad3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=3f8de16dd346c229adf975828e8702b5)
3. **デバイスの選択**
	- 「共有」タブを開く
	- 共有するデバイス（Android）にチェックを入れる
	- 「保存」をクリック  
		[![Pasted image 20251120065021.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/afdd4ef2-4ffc-4ec4-aa6b-7728dc547ec1.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2Fafdd4ef2-4ffc-4ec4-aa6b-7728dc547ec1.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2c013ff11be50d8aa1642ba60c064c98)

#### (2) Android側でフォルダを追加

1. **フォルダの追加通知を確認**
	- Android側のSyncthing-Forkアプリに通知が表示される
	- 通知をタップするか、アプリを開いて「フォルダ」タブを確認
2. **フォルダの設定**
	- 共有されたフォルダをタップ
	- **フォルダパス**: Android内のVaultフォルダを指定
		- 例: `/storage/emulated/0/ObsidianVault`
		- または、フォルダアイコンをタップしてファイルマネージャーで選択
	- **同期タイプ**: 「双方向送受信」（デフォルト）を選択
	- 「保存」をタップ

#### (3) 同期状態の確認

- **PC側**: Web UIの「フォルダ」タブで同期状態を確認
	- 「同期中」: 緑色の矢印アイコン
	- 「同期済み」: 緑色のチェックマーク
- **Android側**: アプリの「フォルダ」タブで同期状態を確認
	- 同期中のファイル数や進捗が表示される

### 5\. 初回同期の確認

#### 同期が開始されたか確認

- **PC側**: Web UIの「フォルダ」タブで同期中のファイル数を確認
- **Android側**: アプリの「フォルダ」タブで同期進捗を確認

初回同期は、Vaultのサイズによって時間がかかることがある。同期が完了するまで待つ。

### 6\. Android側でObsidianをセットアップ

1. **Obsidianアプリをインストール**
	- Google Playストアから「Obsidian」を検索してインストール  
		[![Pasted image 20251120072808.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/71fc8813-a7ac-4e7f-a3ca-6ceeb8252516.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F71fc8813-a7ac-4e7f-a3ca-6ceeb8252516.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=3ff2d53302efada39394f411260bc858)
2. **既存のVaultを開く**
	- Obsidianアプリを起動
	- 「Use my existing vault」を選択  
		[![Pasted image 20251120072859.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/4595dd46-416d-4810-9fc4-25a988e786b3.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F4595dd46-416d-4810-9fc4-25a988e786b3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=63af096e6f004dabcbea439db0e85f73)
	- 「On this device」を選択  
		[![Pasted image 20251120072929.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3692990/529886cb-e19f-4846-a4b3-f90aec4c7b3e.png)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3692990%2F529886cb-e19f-4846-a4b3-f90aec4c7b3e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2fee4657f7e0876a3ac0d9181fe532b1)
	- 「Allow file access」を選択し、ファイルアクセスを許可
	- Syncthingで同期したVaultフォルダを選択
	- 同期したVaultがAndroidで読み込まれたことを確認

### 7\. 使い方

設定完了後は自動同期される。

- **PCで編集** → Androidが自動同期
- **Androidで編集** → PCが自動同期
- **同一Wi-Fi内**: 超高速で直接同期
- **外出先**: インターネット経由で同期（グローバルディスカバリー有効時）

### 外出先からの同期を有効にする

- PC側のSyncthing設定で「グローバルディスカバリー」がONか確認
- デフォルトでグローバルディスカバリーは有効なことが多い
- Android側も同様に確認
- 両方のデバイスがインターネット接続されていれば自動的に発見・同期開始

## 注意点・ベストプラクティス

- **競合回避**: 同時に同じファイルを編集しない（Syncthingは競合が極めて少ない）
- **バックアップ**: 初回同期前にVaultのバックアップを推奨
- **ファイルサイズ**: 大きな画像ファイルが多い場合は同期時間がかかる
- **.obsidianフォルダ**: 設定ファイルも同期されるため、プラグインの互換性に注意
- **バッテリー設定**: Android側でバッテリー最適化を無視する設定が必須

## Syncthingの安全性について

- Obsidian公式が警告するのは「Dropbox/GoogleDriveなどの商用クラウド」
- Syncthingは方式が異なり、ファイル編集検出が正確で衝突が極めて少ない
- Obsidianユーザー間で標準的な無料同期方法
- データはクラウドに保存されず、端末間のみで同期されるためプライバシー面でも優れている

## まとめ

Syncthingを使うことで、ObsidianのVaultをPCとAndroid間で安全かつ高速に同期できます。クラウドストレージを使わず、直接同期するため、プライバシー面でも安心だと思います。初回設定は少し手間がかかりますが、一度設定すれば自動的に同期されるため、非常に便利だと思います。

