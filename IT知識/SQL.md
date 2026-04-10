---
source: https://qiita.com/e-tak/items/fd8703e54363287d0596
published: 2024-10-07
created: 2026-01-28
tags:
  - clippings
  - sql
  - program
---
# **CRUD**（Create, Read, Update, Delete）
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

## 5\. テーブルの作成（CREATE文）
CREATE句*は、「テーブルやユーザーなどのオブジェクトを新しく作成するコマンド」です。  
以下の例では、`book`というテーブルを作成しています。
```
CREATE TABLE book(
    id INT(10) AUTO_INCREMENT NOT NULL,
    name VARCHAR(30) NOT NULL,
    author VARCHAR(30) NOT NULL,
    age INT(3),
    PRIMARY KEY (id)
);
```
「CREATE TABLE」の後ろに「テーブル名」を指定し、（）の中に「カラム名」と「各カラムのデータ型（データの長さ）」を記していく簡単な構文です。

ここで、引数の中には、「テーブルの列名・型・属性」を定義しています。  
具体的に、各引数は下記のような意味を持っています。

- id
    - `INT(10)`: 10桁の整数
    - `AUTO_INCREMENT`: 自動採番
    - `NOT NULL`: 非NULL制約（何かしらのデータを入れないとエラーになる）
    - `PRIMARY KEY`: 主キー
- name
    - `VARCHAR(30)`: 30文字以内の可変長の文字列
    - `NOT NULL`: 非NULL制約（何かしらのデータを入れないとエラーになる）
- author
    - `VARCHAR(30)`: 30文字以内の可変長の文字列
    - `NOT NULL`: 非NULL制約（何かしらのデータを入れないとエラーになる）
- age
    - `INT(3)`: 3桁の整数


# 集計関数