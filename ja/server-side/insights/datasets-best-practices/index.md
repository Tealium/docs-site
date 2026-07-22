---
title: データセットのベストプラクティス
description: この記事では、分析におけるデータセットの作成と管理のベストプラクティスについて説明します。
url: https://docs.tealium.com/ja/server-side/insights/datasets-best-practices/
---
以下のベストプラクティスは、Tealium Insightsでのデータセットのパフォーマンスとデータ品質を確保するのに役立ちます。

## データセット構造の最適化

データセットの構造を最適化することで、クエリのパフォーマンスを大幅に向上させ、ロード時間を短縮することができます。

### 複数の小さなデータセットを使用する

ダッシュボードに一つの大きなデータセットを使用する代わりに、それを複数の小さなデータセットに分割します。小さなデータセットを使用することで、一度にロードされるデータが減少し、クエリが速くなり、ダッシュボードがより反応性を持つようになります。

### 列の数を減らす

[データセットを作成する](https://docs.tealium.com/manage-datasets/#create-a-new-dataset)際には、デフォルトですべての列がSPICE（Super-fast Parallel In-memory Calculation Engine）にロードされます。必要以上に多くの列を含めると、特に大きなデータセットではクエリのパフォーマンスが低下します。

例えば、2000万行のデータセットでは：
* 1列をロードするのに約 `2.63` 分かかります。
* 4列をロードするのに約 `4.61` 分かかります。
* 150列をロードするのに約 `19.49` 分かかります。

データセットビューでは、分析やダッシュボードに必要な列のみを含め、不要な列は削除します。これにより、ロード時間が短縮され、反応性が向上します。

![](https://docs.tealium.com/images/server-side/data-insights/include-and-exclude-columns-in-datasets.png)

## 日付列を使用して行をフィルタリングする

大きなデータセットでは、日付列を使用して行をフィルタリングすることで、データベースのパフォーマンスを大幅に向上させることができます。
* イベントデータの場合、`event - time` 列でフィルタリングします。
* 訪問/訪問データの場合、`updated` 列でフィルタリングします。

これらの日付列でフィルタリングすることで、Insightsはソートの最適化を活用でき、データの取得が速くなります。

## SQLを使用してデータを集約し、処理する

### カスタムSQLを使用する

全テーブルやスキーマをロードする代わりに、**カスタムSQL**オプションを使用して、データをSPICEにロードする前にデータを事前集約したりフィルタリングしたりします。これにより、データセットのサイズが縮小し、パフォーマンスが向上します。

例えば、イベントタイプを日ごとにカウントするには、次のようなSQLクエリを使用します：

```sql
SELECT 
    COUNT(*) AS count, 
    TRUNC("event - time") AS "period", 
    "event - udo - tealium_event" 
FROM ${db_schema}.events_view__all_events__all_events 
GROUP BY "period", "event - udo - tealium_event";
```

このアプローチを、SPICEで処理するデータを減らすために、他の集約や分析にも適応させます。

### クエリで `SELECT *` を使用しない

`SELECT *` クエリを使用すると、パフォーマンスが低下し、クエリが読みにくくなります。代わりに、必要な列のみを選択します。

すべての列を選択するのを避けます：
```sql
SELECT * FROM employees;
```

必要な列のみを選択します：
```sql
SELECT employee_id, first_name, last_name
FROM employees;
```

新しいテーブルを探索してすべての列を見る必要がある場合は、表示される行数を減らすために `LIMIT` 句を使用します：

```sql
SELECT * FROM employees
LIMIT 10;
```

### サブクエリを避ける

サブクエリは柔軟なクエリの組織を提供しますが、パフォーマンスを低下させる可能性があります。可能な場合は、結合や一時テーブルを使用します。

サブクエリを使用するのを避けます： 
```sql
SELECT employee_id, first_name, last_name
FROM employees
WHERE department_id IN (SELECT id FROM departments WHERE name = 'Sales');
```

2つのテーブルからデータをクエリするために結合を使用します：
```sql
SELECT e.employee_id, e.first_name, e.last_name, d.department_name
FROM employees e
JOIN departments d ON e.department_id = d.id
WHERE d.name = 'Sales';
```

## 増分リフレッシュを構成する

データセットの精度を維持し、リフレッシュ時間を短縮するために、リフレッシュスケジュールを作成する際に増分リフレッシュを構成します。増分リフレッシュは、新規または更新されたデータのみを処理するため、大規模で頻繁に更新されるデータセットに最適です。これに対して、フルリフレッシュはデータセット全体を再ロードします。最適な結果を得るために、ウィンドウサイズは2日を推奨しますが、要件に応じて調整することができます。

![](https://docs.tealium.com/images/server-side/data-insights/configure-incremental-refresh.png)