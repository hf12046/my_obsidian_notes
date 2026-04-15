---
source: https://qiita.com/e-tak/items/fd8703e54363287d0596
published: 2024-10-07
created: 2026-01-28
tags:
  - clippings
  - sql
  - program
---
## 1. CREATE（データの作成）

**テーブルの作成**
```sql
CREATE TABLE employees (
    id       INTEGER PRIMARY KEY,
    name     TEXT NOT NULL,
    dept     TEXT,
    salary   INTEGER DEFAULT 0,
    hired_at DATE
);
```

**データの挿入（INSERT）**
```sql
-- 1行挿入
INSERT INTO employees (name, dept, salary, hired_at)
VALUES ('田中太郎', '営業', 350000, '2024-04-01');

-- 複数行を一括挿入
INSERT INTO employees (name, dept, salary, hired_at)
VALUES
    ('佐藤花子', '開発', 400000, '2024-04-01'),
    ('鈴木一郎', '人事', 320000, '2024-05-15');
```

---
## 2. READ（データの取得）

**基本の SELECT**
```sql
-- 全列取得
SELECT * FROM employees;

-- 特定の列だけ取得
SELECT name, salary FROM employees;

-- 条件付き（WHERE）
SELECT * FROM employees WHERE dept = '開発';

-- 並び替え（ORDER BY）
SELECT * FROM employees ORDER BY salary DESC;

-- 件数制限（LIMIT）
SELECT * FROM employees ORDER BY hired_at DESC LIMIT 5;
```

**よく使う比較・論理演算子**
```sql
WHERE salary >= 300000                  -- 比較
WHERE dept IN ('営業', '開発')           -- 複数値マッチ
WHERE name LIKE '田中%'                 -- 前方一致
WHERE hired_at BETWEEN '2024-01-01'
                 AND '2024-12-31'       -- 範囲指定
WHERE dept = '開発' AND salary > 350000 -- AND条件
WHERE dept = '営業' OR dept = '人事'    -- OR条件
WHERE email IS NULL                     -- NULLチェック
```

**テーブル結合（JOIN）**
```sql
-- 部署テーブルと内部結合
SELECT e.name, d.dept_name, e.salary
FROM employees e
INNER JOIN departments d ON e.dept_id = d.id;

-- LEFT JOINは右側にデータがなくてもNULLで返す
SELECT e.name, p.project_name
FROM employees e
LEFT JOIN projects p ON e.id = p.leader_id;
```

---
## 3. UPDATE（データの更新）
```sql
-- 特定の行を更新
UPDATE employees
SET salary = 380000
WHERE name = '田中太郎';

-- 条件に合う複数行を一括更新
UPDATE employees
SET salary = salary * 1.05
WHERE dept = '開発';
```

> **注意:** `WHERE` を忘れると全行が更新されるため、必ず条件を指定してください。

---
## 4. DELETE（データの削除）
```sql
-- 条件に合う行を削除
DELETE FROM employees WHERE id = 3;

-- 全行削除（テーブル構造は残る）
DELETE FROM employees;
```

> **注意:** UPDATE と同様、`WHERE` を忘れると全行が消えます。

---
## 5. 集計関数・句（Aggregate）

**主要な集計関数**
```sql
SELECT
    COUNT(*)        AS 全件数,
    COUNT(DISTINCT dept) AS 部署数,
    SUM(salary)     AS 給与合計,
    AVG(salary)     AS 給与平均,
    MAX(salary)     AS 最高給与,
    MIN(salary)     AS 最低給与
FROM employees;
```

**GROUP BY + HAVING**
```sql
-- 部署ごとの集計（3人以上の部署のみ）
SELECT
    dept,
    COUNT(*)   AS 人数,
    AVG(salary) AS 平均給与
FROM employees
GROUP BY dept
HAVING COUNT(*) >= 3
ORDER BY 平均給与 DESC;
```

---
## 6. SQL の処理順序

書く順序と処理される順序は異なります。

```
処理順:  FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
記述順:  SELECT → FROM → WHERE → GROUP BY → HAVING → ORDER BY → LIMIT
```

WHEREは「集計前に行を絞る」、HAVINGは「集計後に結果を絞る」と覚えておくのがポイントです。

---
## 7. 組み合わせた実践例
```sql
-- 部署別・年別の採用人数と平均給与（2名以上採用した組み合わせのみ）
SELECT
    dept,
    strftime('%Y', hired_at) AS hire_year,
    COUNT(*)                 AS hire_count,
    AVG(salary)              AS avg_salary
FROM employees
WHERE hired_at IS NOT NULL
GROUP BY dept, hire_year
HAVING COUNT(*) >= 2
ORDER BY hire_year, dept;
```

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