---
source: https://qiita.com/e-tak/items/fd8703e54363287d0596
published: 2024-10-07
created: 2026-01-28
tags:
  - clippings
  - sql
  - program
---
# CRUD（Create, Read, Update, Delete）
## データの抽出（SELECT文）
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

## データの追加（INSERT文）
新しいデータをデータベースに追加するには、`INSERT` 文を使用します。  
例えば、以下のように書くことで、新しいユーザーを `users` テーブルに追加できます。
```sql
INSERT INTO users (name, email, age) VALUES ('Test Taro', 'taro@example.com', 25);
```

これにより、 `name` 、 `email` 、 `age` のフィールドにデータが追加されます。  
  
ここでテーブルには上記以外に `Adress` という項目があったとします。  
値を設定しているのは上記3項目以外のフィールドのみのため、値を設定していない `Adress` はどうなるかというと、  
テーブル定義によっても異なりますが初期値（ `null` や `0` など）が設定されます。

## データの更新（UPDATE文）
既存のデータを更新したい場合は、`UPDATE` 文を使用します。  
例えば、特定のユーザーのメールアドレスを更新するには以下のようにします。
```sql
UPDATE users SET email = 'tarotaro@example.com' WHERE name = 'Test Taro';
```

このクエリは、名前が `Test Taro` であるユーザーのメールアドレスを更新します。  
`WHERE` 句を忘れると全てのレコードが更新の対象になってしまうため注意しましょう。  
また、仮に同テーブル上に同姓同名の `Test Taro` が複数存在した場合、更新対象も複数となります。  
対象レコード1レコードのみ更新したい場合には、テーブルごとに一意になる主キー（PRIMARY KEY）などを用いて対応するようにします。

## データの削除（DELETE文）
不要なデータを削除するには、`DELETE` 文を使用します。  
例えば、特定のユーザーを削除する場合は次のようにします。
```sql
DELETE FROM users WHERE name = 'Test Taro';
```

このクエリは、 `name` が `Test Taro` であるユーザーをデータベースから削除します。

## テーブルの作成（CREATE文）
`CREATE` 句は、「テーブルやユーザーなどのオブジェクトを新しく作成するコマンド」です。  
以下の例では、`book`というテーブルを作成しています。
```sql
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

---

# 集計関数
集計関数とは、複数行のデータをまとめて1つの値を返す関数です。

## 主な集計関数一覧

| 関数 | 説明 |
|------|------|
| `COUNT()` | 行数を数える |
| `SUM()` | 合計値を求める |
| `AVG()` | 平均値を求める |
| `MAX()` | 最大値を求める |
| `MIN()` | 最小値を求める |

## COUNT
テーブルの行数を取得します。
```sql
-- 全行数を取得
SELECT COUNT(*) FROM users;

-- NULLを除いた特定カラムの行数を取得
SELECT COUNT(email) FROM users;
```

## SUM
数値カラムの合計を取得します。
```sql
-- 全ユーザーの年齢合計
SELECT SUM(age) FROM users;
```

## AVG
数値カラムの平均を取得します。
```sql
-- 全ユーザーの平均年齢
SELECT AVG(age) FROM users;
```

## MAX / MIN
最大値・最小値を取得します。
```sql
-- 最年長・最年少のユーザーの年齢
SELECT MAX(age), MIN(age) FROM users;
```

---

# グループ化（GROUP BY）
`GROUP BY` 句を使うと、指定したカラムの値ごとにデータをまとめて集計できます。

## 基本構文
```sql
SELECT カラム名, 集計関数
FROM テーブル名
GROUP BY カラム名;
```

## 使用例
```sql
-- 都市ごとのユーザー数を集計
SELECT city, COUNT(*) AS user_count
FROM users
GROUP BY city;
```

```sql
-- 部署ごとの平均給与を集計
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

`GROUP BY` で指定していないカラムを `SELECT` に含める場合は、必ず集計関数で囲む必要があります。

---

# グループ化後の絞り込み（HAVING）
`WHERE` 句はグループ化の前に行数を絞り込みますが、`HAVING` 句はグループ化した後の集計結果に対して条件を指定します。

## WHERE との違い

| 句 | 適用タイミング | 集計関数の使用 |
|----|--------------|--------------|
| `WHERE` | グループ化の前（行単位） | 使用不可 |
| `HAVING` | グループ化の後（グループ単位） | 使用可能 |

## 基本構文
```sql
SELECT カラム名, 集計関数
FROM テーブル名
GROUP BY カラム名
HAVING 条件;
```

## 使用例
```sql
-- ユーザー数が5人以上の都市のみ取得
SELECT city, COUNT(*) AS user_count
FROM users
GROUP BY city
HAVING COUNT(*) >= 5;
```

```sql
-- 平均給与が50万円以上の部署を取得
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING AVG(salary) >= 500000;
```

## WHERE と HAVING の組み合わせ
`WHERE` でグループ化前に絞り込み、`HAVING` でグループ化後にさらに絞り込むこともできます。
```sql
-- 30歳以上のユーザーのみを対象に、都市ごとに集計し、5人以上の都市を取得
SELECT city, COUNT(*) AS user_count
FROM users
WHERE age >= 30
GROUP BY city
HAVING COUNT(*) >= 5;
```

## SELECT文の実行順序
SQLは記述順ではなく、以下の順序で処理されます。

```
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```

この順序を意識すると、どの句でどの絞り込みを行うべきかが分かりやすくなります。