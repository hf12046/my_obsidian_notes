---
title: SQLの基礎を学ぼう！データベース操作の基本
source: https://qiita.com/e-tak/items/fd8703e54363287d0596
published: 2024-10-07
created: 2026-01-28
description: ■ はじめに この記事では、SQLの基礎を解説します。 これからSQLを学ぶ方や、基礎を再確認したい方はこの記事でSQLの基本操作を一緒に見ていきましょう。 データベース操作の検索、追加、更新、削除の基本操作をサンプルコードで説明します。 ■ 目次 SQLとは ...
tags:
  - clippings
  - sql
  - program
---
## ■ 目次  
1. [データの抽出（SELECT文）](https://qiita.com/e-tak/items/#2-%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E6%A4%9C%E7%B4%A2select%E6%96%87)
2. [データの追加（INSERT文）](https://qiita.com/e-tak/items/#3-%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E8%BF%BD%E5%8A%A0insert%E6%96%87)
3. [データの更新（UPDATE文）](https://qiita.com/e-tak/items/#4-%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E6%9B%B4%E6%96%B0update%E6%96%87)
4. [データの削除（DELETE文）](https://qiita.com/e-tak/items/#5-%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E5%89%8A%E9%99%A4delete%E6%96%87)

## 1\. データの抽出（SELECT文）
以下のように書くことでテーブル`users`から全てのデータを取得できます。
```sql
SELECT * FROM users;
```

テーブル `users` から特定のカラムだけを取得したい場合は、カラム名を指定します。
```sql
SELECT name, email FROM users;
```

条件を絞るためには、 `WHERE` 句を使用します。
```sql
SELECT * FROM users WHERE age >= 20;
```

このクエリでは、age というカラムが20以上の場合のみ取得することができるので、  
20歳以上のユーザーのみが取得できることになります。

## 2\. データの追加（INSERT文）
新しいデータをデータベースに追加するには、`INSERT` 文を使用します。  
例えば、以下のように書くことで、新しいユーザーを `users` テーブルに追加できます。
```sql
INSERT INTO users (name, email, age) VALUES ('Test Taro', 'taro@example.com', 25);
```

これにより、 `name` 、 `email` 、 `age` のフィールドにデータが追加されます。  
  
ここでテーブルには上記以外に `Adress` という項目があったとします。  
値を設定しているのは上記3項目以外のフィールドのみのため、値を設定していない `Adress` はどうなるかというと、  
テーブル定義によっても異なりますが初期値（ `null` や `0` など）が設定されます。

## 3\. データの更新（UPDATE文）
既存のデータを更新したい場合は、\`UPDATE\`文を使用します。  
例えば、特定のユーザーのメールアドレスを更新するには以下のようにします。
```sql
UPDATE users SET email = 'tarotaro@example.com' WHERE name = 'Test Taro';
```

このクエリは、名前が `Test Taro` であるユーザーのメールアドレスを更新します。  
`WHERE` 句を忘れると全てのレコードが更新の対象になってしまうため注意しましょう。  
また、仮に同テーブル上に同姓同名の `Test Taro` が複数存在した場合、更新対象も複数となります。  
対象レコード1レコードのみ更新したい場合には、テーブルごとに一意になる主キー（PRIMARY KEY）などを用いて対応するようにします。

## 4\. データの削除（DELETE文）  
不要なデータを削除するには、\`DELETE\` 文を使用します。  
例えば、特定のユーザーを削除する場合は次のようにします。
```sql
DELETE FROM users WHERE name = 'Test Taro';
```

このクエリは、 `name` が `Test Taro` であるユーザーをデータベースから削除します。