---
title: AudienceDBデータガイド
description: この記事では、Tealium DataAccess AudienceDB内で利用可能なデータについて説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/audiencedb-data-guide/
---
## 動作原理

AudienceDBは、訪問レベルと訪問レベルのデータをAmazon Redshift™のPostgres風データベースに保存し、お好みのSQLクライアントやビジネスインテリジェンス（BI）ツールを使用してデータを直接クエリして分析することができます。

AudienceDBがアクティブになると、AudienceStreamデータを保存するためのデータベースがAmazon Redshift™に作成されます。新しいデータベースには、保存可能な各データタイプのテーブルが含まれています。訪問レベルのデータに関連するデータは、`visit_`で始まるテーブルに保存され、訪問レベルのデータに関連するデータは、`visitor_`で始まるテーブルに保存されます。テーブルに加えて、クエリの作成を容易にするためにいくつかのビューも作成されます。

AudienceDBが初めての方は、[AudienceDBとEventDBの操作]()の基本を確認してください。

## EventDBとAudienceDBの図

イベント、訪問、訪問属性はEventDBとAudienceDBで連携して動作します。以下の図は、EventDBとAudienceDBの属性間の関係を示しています。これらの関係は、特定の訪問または訪問のイベントデータを返すクエリを書く際に重要です。

![](/images/server-side/eventdb-and-audiencedb-diagram.jpg)

## 属性と列名

AudienceDBで有効になっている各訪問および訪問属性は、データベーステーブルの一つ以上の列として表示されます。

以下は、属性データタイプと対応する列名の命名規則のリストです。「###」は属性IDを表します。表に示されている例は訪問属性を示しています。訪問属性は「visitor」の代わりに「visit」という単語を使用します。

|属性データタイプ| テーブル列名|
|---| ---|
|配列|  &lt;ul&gt;&lt;li&gt;**テーブル**: `array_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor array - array_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor array - array_name`&lt;/li&gt;&lt;/ul&gt; |
|オーディエンス&lt;br&gt; `t`は真、`f`は偽を示し、オーディエンスに存在するかを示します。|  &lt;ul&gt;&lt;li&gt;**テーブル**: `audience_account_profile_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor - audience - audience_name (account_profile_###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor - audience - audience_name`&lt;/li&gt;&lt;/ul&gt; |
|バッジ&lt;br&gt; `t`は真、`f`は偽を示し、バッジの存在を示します。|  &lt;ul&gt;&lt;li&gt;**テーブル**: `badge_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor - badge - badge_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor - badge - badge_name`&lt;/li&gt;&lt;/ul&gt; |
|ブール値|  &lt;ul&gt;&lt;li&gt;**テーブル**: `flag_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor - flag - boolean_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor - flag - boolean_name`&lt;/li&gt;&lt;/ul&gt; |
|日付|  &lt;ul&gt;&lt;li&gt;**テーブル**: `date_###`&lt;/li&gt;&lt;/ul&gt; &lt;ul&gt;&lt;li&gt;**ビュー**: `visitor - date - date_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor - date - date_name`&lt;/li&gt;&lt;/ul&gt; |
|数値|  &lt;ul&gt;&lt;li&gt;**テーブル**: `metric_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor - metric - metric_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor - metric - metric_name`&lt;/li&gt;&lt;/ul&gt; |
|文字列のセット|  &lt;ul&gt;&lt;li&gt;**テーブル**: `list_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor list - set_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor list - set_name`&lt;/li&gt;&lt;/ul&gt; |
|文字列|  &lt;ul&gt;&lt;li&gt;**テーブル**: `property_###`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor - property - property_name (###)`&lt;/li&gt;&lt;li&gt;**正規化**: `visitor - property - property_name`&lt;/li&gt;&lt;/ul&gt; |
|集計|  &lt;ul&gt;&lt;li&gt;**テーブル**: `visitor_tally_###_key` `visitor_tally_###_value`&lt;/li&gt;&lt;li&gt;**ビュー**: `visitor tally - tally_name (###) - key` &#34;visitor tally - tally_name (###) - value&#34;&lt;/li&gt;&lt;li&gt;**正規化**: `visitor tally - tally_name - key` &#34;visitor tally - tally_name - value&#34;&lt;/li&gt;&lt;/ul&gt; |

## AudienceDBテーブル

以下の表は、オーディエンスデータに使用されるAudienceDBテーブルタイプと、対応する「ビュー」と「正規化」テーブルの名前を説明しています：

|データタイプと説明| テーブル/ビュー/正規化名|
|---| ---|
|**配列**&lt;br&gt; 配列の各アイテムは、`index`という名前の追加列を持つテーブルの行です。| `visit_arrays`&lt;br&gt; `visit_arrays_view`&lt;br&gt; `visitor_arrays`&lt;br&gt; `visitor_arrays_view`&lt;br&gt; `visitor_arrays_view_normalized`|
|**文字列のセット**&lt;br&gt; セットの各アイテムはテーブルの行です。| `visit_lists`&lt;br&gt; `visit_lists_view`&lt;br&gt; `visitor_lists`&lt;br&gt; `visitor_lists_view`&lt;br&gt; `visitor_lists_view_normalized`|
|**集計**&lt;br&gt; 集計の各アイテムは、キー（接尾辞 `_key`）と値（接尾辞 `_value`）の1つの列を持つテーブルの行です。| `visit_tallies`&lt;br&gt; `visit_tallies_view`&lt;br&gt; `visitor_tallies`&lt;br&gt; `visitor_tallies_view`&lt;br&gt; `visitor_tallies_view_normalized`|
|**ステッチされた訪問**&lt;br&gt; プロファイルの一部としてステッチされた訪問ID。| `visitor_replaces`&lt;br&gt; `visitor_replaces_view`|
|**訪問**&lt;br&gt; 現在の訪問属性と所属するオーディエンス。| `visits`&lt;br&gt; `visits_view`|
|**訪問**&lt;br&gt; 訪問属性と所属するオーディエンス。| `visitors`&lt;br&gt; `visitors_view`&lt;br&gt; `visitors_view_normalized`|
|**訪問バッチ** | 内部使用のみ|

### 訪問テーブル、ビュー、および正規化ビュー

AudienceDBは訪問データをテーブル、ビュー、および正規化ビューとして公開します。それぞれは異なる目的を持っています。

| テーブル/ビュー名 | 説明 |
|---|---|
| `visitors` (テーブル) | 各訪問のすべての履歴行を含み、すべての状態変更を含みます。列名は属性IDを使用します（例：`badge_30`, `flag_5052`）。このテーブルは監査および時間経過による変更のクエリに使用します。 |
| `visitors_view` (ビュー) | 最新の状態のみを含みます（訪問ごとに1行）。列名は属性IDと名前を使用します（例：`visitor - badge - VIP (13)`）。このビューは現在の状態のレポートに使用します。 |
| `visitors_view_normalized` (正規化ビュー) | `visitors_view`と同じ行を含みますが、列名は属性IDを省略します（例：`visitor - badge - VIP`）。このビューはBIツールや、列名が一貫している必要がある安定したダッシュボードに使用します。 |
| `visitor_replaces` (テーブル) | ステッチされた訪問IDマッピングのすべてのバージョンを含み、置換されたIDも含みます。このテーブルは完全なステッチ履歴に使用します。 |
| `visitor_replaces_view` (ビュー) | 最新の、置換されていない訪問IDのみを含みます。このビューは訪問IDを現在のプロファイルに解決するために使用します。 |

### 訪問テーブル、ビュー、および正規化ビュー

AudienceDBは訪問データをテーブル、ビュー、および正規化ビューとして公開します。それぞれは異なる目的を持っています。

| テーブル/ビュー名 | 説明 |
|---|---|
| `visitors` (テーブル) | 各訪問のすべての履歴行を含み、すべての状態変更を含みます。列名は属性IDを使用します（例：`badge_30`, `flag_5052`）。このテーブルは監査および時間経過による変更のクエリに使用します。 |
| `visitors_view` (ビュー) | 最新の状態のみを含みます（訪問ごとに1行）。列名は属性IDと名前を使用します（例：`visitor - badge - VIP (13)`）。このビューは現在の状態のレポートに使用します。 |
| `visitors_view_normalized` (正規化ビュー) | `visitors_view`と同じ行を含みますが、列名は属性IDを省略します（例：`visitor - badge - VIP`）。このビューはBIツールや、列名が一貫している必要がある安定したダッシュボードに使用します。 |
| `visitor_replaces` (テーブル) | ステッチされた訪問IDマッピングのすべてのバージョンを含み、置換されたIDも含みます。このテーブルは完全なステッチ履歴に使用します。 |
| `visitor_replaces_view` (ビュー) | 置換されていない最新の訪問IDのみを含みます。このビューは訪問IDを現在のプロファイルに解決するために使用します。 |

## サンプルデータベース構造

以下のセクションでは、各ビューのサンプル構造例を提供し、各ビューが何がユニークであり、他のビューとどのように異なるかを判断するのに役立ちます。

### 訪問配列

以下の例は、`visit_arrays`テーブルの基本的なフォーマットを示しています：

```nohl
 visit_id                          | index | updated                 | visit_array_421
 ----------------------------------&#43;--------------------------------------------------------------------------
 13e1a63890793caa346f90607a76c1c98 | 0     | 2018-05-17 01:03:30.344 | スマートフォン
 13e1a63890793caa346f90607a76c1c98 | 1     | 2018-05-17 01:03:30.344 | フォンチャージャー
 13e1a63890793caa346f90607a76c1c98 | 2     | 2018-05-17 01:03:30.344 | スマートフォンケース
```

### 訪問リスト

以下の例は、`visit_lists`テーブルの基本的なフォーマットを示しています：

```nohl
myexample=# select visit_id, updated, visit_list_284 from visit_lists;

 visit_id                          | updated                 | visit_list_284
 ----------------------------------&#43;-------------------------------------------------------------------------
 13e1a63890793caa346f90607a76c1c98 | 2018-04-22 12:50:20.471 | 携帯電話 &amp; アクセサリ
 13e1a63890793caa346f90607a76c1c98 | 2018-04-22 12:50:20.471 | コンピュータとタブレット
 13e1a63890793caa346f90607a76c1c98 | 2018-04-22 12:50:20.471 | オフィス用品
```
### 訪問数の集計

以下の例は、`visitor_tallies` テーブルの基本的なフォーマットを示しています：

```nohl
myexample=# select visit_id, updated, visit_tally_5144_key, visit_tally_5144_value from visit_tallies;

                        visit_id                                 | updated                 | visit_tally_5144_key | visit_tally_5144_value
-----------------------------------------------------------------&#43;-------------------------&#43;----------------------&#43;-----------------------
19fd8716d2f8341b81f84f471b5f950873d5c88acee9c61089f286fb8b5d4903 | 2017-09-04 20:39:05.303 | Furniture            | 2
06db172cf2a8fd7f9ff882a28a14ad266ee67824c9bc3ee0b1fcc451b42cec68 | 2017-09-05 06:20:16.209 | Furniture            | 14
162e22ba6c168bff2385bcfba9d4ba8e15767d1ad8b519b3a872a2ad89d3f3dd | 2017-09-05 06:04:59.671 | Search               | 2
4225575ce21a7f9454c56c269eccfee9782e03c6f647a743f058b7b667dd3bbb | 2017-09-20 06:30:14.63  | Home                 | 1
e1e5dd5e58bc97056f8340e242205e1ec2ab0a88c94c890563399f55828638f7 | 2017-09-09 14:22:08.575 | Furniture            | 3
(5 rows)
```

### 訪問配列ビュー

以下の例は、`visitor_arrays_view` テーブルの基本的なフォーマットを示しています：

```nohl
myexample=# select &#34;visitor - id&#34;, &#34;index&#34;, &#34;updated&#34;, &#34;visitor array - cart product name (421)&#34; from visitor_arrays_view;

 &#34;visitor array - visitor id&#34;      | index | updated                 | &#34;visitor array - cart product name (421)&#34;
 ----------------------------------&#43;--------------------------------------------------------------------------
 13e1a63890793caa346f90607a76c1c98 | 0     | 2018-05-17 01:03:30.344 | Smartphone
 13e1a63890793caa346f90607a76c1c98 | 1     | 2018-05-17 01:03:30.344 | Phone Charger
 13e1a63890793caa346f90607a76c1c98 | 2     | 2018-05-17 01:03:30.344 | Smartphone Case

```

### 訪問リスト

以下の例は、`visitor_lists` テーブルの基本的なフォーマットを示しています：

```nohl
myexample=# select visitor_id, updated, visitor_list_5168 from visitor_lists;

                  visitor_id                   |         updated         | visitor_list_5168
-----------------------------------------------&#43;-------------------------&#43;-------------------
 015e94db670900084e37016b9b7300087002f07f00432 | 2017-11-04 13:30:33.553 | Cell Phones
 015e94db670900084e37016b9b7300087002f07f00432 | 2017-11-04 13:30:33.553 | Phone Accessories
 015e94db670900084e37016b9b7300087002f07f00432 | 2017-11-04 13:30:33.553 | Office Supplies

```

### 訪問置換

以下の例は、`visitor_replaces` テーブルの基本的なフォーマットを示しています：

```nohl
myexample=# select visitor_replaces_id, visitor_id, updated from visitor_replaces where updated is not null;

                visitor_replaces_id           | visitor_id                                      | updated
----------------------------------------------&#43;-------------------------------------------------&#43;------------------------
015f8d82498b00132b921ecf890d00089001c08100432 | myexample_main__5216_username@gmail.com         | 2017-11-23 15:32:28.81
015f4a0302b9009e17205a49027005079001c07100c48 | myexample_main__5216_username@myexample.com     | 2017-11-24 22:50:31.105
015feb1537cc00305e319fca622400085001d07d00720 | myexample_main__5216_username@yahoo.com         | 2017-11-26 01:22:27.57
015decf4f3170011afb0979834420007e007b07600720 | myexample_main__5216_username@hotmail.com       | 2018-01-03 22:03:20.837
015e3b903e48000c7944f6af4b8e00087016907f0049e | myexample_main__5216_username@cox.net           | 2018-01-28 03:59:45.031
(5 rows)
```
## スティッチされた訪問の理解

AudienceDBでは、スティッチされた訪問に対して訪問テーブルには1つの訪問プロファイルのみが保持されます。スティッチされた訪問のプロファイルは1つとして見られますが、異なるIDを持っています。`visitor_replaces`テーブルは、この目的を達成するために置き換えられた`visitor_ids`を見るためのルックアップ方法を提供します。

Visitor Replacesテーブルの例：

|`visitor_replaces_id`| `visitor_id`|
|---| ---|
|1| 3|
|2| 3|
|4| 6|
|5| 6|

このテーブルでは：

* Visitor1とVisitor2はVisitor3にスティッチされます。
* Visitor4とVisitor5はVisitor6にスティッチされます。

上記の情報は、必要に応じて`visitors`テーブルを`visits`テーブルまたはEventDBのテーブルと結合するために使用できます。

EventDBのイベントをAudienceDBに結合するには：

* スティッチされていない訪問については、`events_x`を`visitors`テーブルに直接結合し、
* スティッチされた訪問については、次の例に示すように`visitor_replaces`テーブルを介して結合します：

```sql
SELECT e.&#34;event - id&#34;, v.&#34;visitor - id&#34;
FROM account__profile.events_view__all_events__all_events e
LEFT JOIN account__profile.visitor_replaces_view r ON e.&#34;event - visitor id&#34; = r.&#34;visitor - replaces id&#34;
JOIN account__profile.visitors_view_normalized v ON (v.&#34;visitor - id&#34; = r.&#34;visitor - id&#34; or v.&#34;visitor - id&#34; = e.&#34;event - visitor id&#34;)
limit 1000;
```

* この例では、`events_all_events`の訪問IDが`visitors`または`visitor_replaces`にあることを考慮しています。
単一のイベントセッションに帰属する訪問は訪問テーブルには保存されません。

## 追加のリソース

* [(Amazon Redshift™) クエリ設計のベストプラクティス](https://docs.aws.amazon.com/redshift/latest/dg/c_designing-queries-best-practices.html)
* [(Amazon Redshift™) クエリパフォーマンスのチューニング](https://docs.aws.amazon.com/redshift/latest/dg/c-optimizing-query-performance.html)