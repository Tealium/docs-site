---
title: AudienceDB データガイド
description: この記事では、Tealium DataAccess AudienceDB で利用できるデータについて説明します。
url: https://docs.tealium.com/ja/server-side/data-storage/audiencedb-eventdb/audiencedb-data-guide/
---
## 仕組み

AudienceDB は、訪問レベルと訪問レベルの両方のデータを、Amazon Redshift™ 内の Postgres に似たデータベースに保存します。任意の SQL クライアントまたはビジネスインテリジェンス（BI）ツールを使用して、データを直接クエリおよび分析できます。

AudienceDB を有効にすると、Customer Data Platform（CDP）データを保存するためのデータベースが Amazon Redshift™ に作成されます。新しいデータベースには、保存可能な各データタイプに対応するテーブルが含まれます。訪問レベルのデータに関連するデータは、接頭辞 `visit_` が付いたテーブルに保存されます。訪問レベルのデータに関連するデータは、接頭辞 `visitor_` が付いたテーブルに保存されます。また、クエリを簡単に作成できるように、テーブルに加えて複数のビューも作成されます。

AudienceDB を初めて使用する場合は、[AudienceDB と EventDB の操作](https://docs.tealium.com/audiencedb-and-eventdb/)で基本事項を確認してください。

## EventDB と AudienceDB の図

イベント、訪問、訪問の各属性は、EventDB と AudienceDB で連携して機能します。次の図は、EventDB と AudienceDB の属性間の関係を示しています。これらの関係は、特定の訪問または訪問に関するイベントデータを返すクエリを作成する際に重要です。

![](https://docs.tealium.com/images/server-side/eventdb-and-audiencedb-diagram.jpg)

## 属性と列名

AudienceDB で有効になっている各訪問属性および訪問属性は、1 つ以上のデータベーステーブルに列として表示されます。

次に、属性のデータタイプと対応する列の命名規則を示します。「###」は属性 ID を表します。表に示す例は訪問属性です。訪問属性では、「visitor」の代わりに「visit」を使用します。

|属性のデータタイプ|テーブルの列名|
|---| ---|
|配列|<ul><li>**テーブル**: `array_###`</li><li>**ビュー**: `visitor array - array_name (###)`</li><li>**正規化**: `visitor array - array_name`</li></ul> |
|オーディエンス<br> true を表す値 `t` と false を表す値 `f` は、オーディエンスに属しているかどうかを示します。|<ul><li>**テーブル**: `audience_account_profile_###`</li><li>**ビュー**: `visitor - audience - audience_name (account_profile_###)`</li><li>**正規化**: `visitor - audience - audience_name`</li></ul> |
|バッジ<br> true を表す値 `t` と false を表す値 `f` は、バッジの有無を示します。|<ul><li>**テーブル**: `badge_###`</li><li>**ビュー**: `visitor - badge - badge_name (###)`</li><li>**正規化**: `visitor - badge - badge_name`</li></ul> |
|ブール値|<ul><li>**テーブル**: `flag_###`</li><li>**ビュー**: `visitor - flag - boolean_name (###)`</li><li>**正規化**: `visitor - flag - boolean_name`</li></ul> |
|日付|<ul><li>**テーブル**: `date_###`</li></ul> <ul><li>**ビュー**: `visitor - date - date_name (###)`</li><li>**正規化**: `visitor - date - date_name`</li></ul> |
|数値|<ul><li>**テーブル**: `metric_###`</li><li>**ビュー**: `visitor - metric - metric_name (###)`</li><li>**正規化**: `visitor - metric - metric_name`</li></ul> |
|文字列セット|<ul><li>**テーブル**: `list_###`</li><li>**ビュー**: `visitor list - set_name (###)`</li><li>**正規化**: `visitor list - set_name`</li></ul> |
|文字列|<ul><li>**テーブル**: `property_###`</li><li>**ビュー**: `visitor - property - property_name (###)`</li><li>**正規化**: `visitor - property - property_name`</li></ul> |
|集計|<ul><li>**テーブル**: `visitor_tally_###_key` `visitor_tally_###_value`</li><li>**ビュー**: `visitor tally - tally_name (###) - key` "visitor tally - tally_name (###) - value"</li><li>**正規化**: `visitor tally - tally_name - key` "visitor tally - tally_name - value"</li></ul> |

## AudienceDB テーブル

次の表では、オーディエンスデータに使用される AudienceDB テーブルのタイプと、対応する「ビュー」および「正規化」テーブルの名前について説明します。

|データタイプと説明|テーブル／ビュー／正規化の名前|
|---| ---|
|**配列**<br>配列内の各項目はテーブル内の 1 行となり、ゼロから始まる配列位置を示す `index` という名前の列が追加されます。| `visit_arrays`<br> `visit_arrays_view`<br> `visitor_arrays`<br> `visitor_arrays_view`<br> `visitor_arrays_view_normalized`|
|**文字列セット**<br>セット内の各項目は、テーブル内の 1 行になります。| `visit_lists`<br> `visit_lists_view`<br> `visitor_lists`<br> `visitor_lists_view`<br> `visitor_lists_view_normalized`|
|**集計**<br>集計内の各項目はテーブル内の 1 行となり、キー用の列（接尾辞 `_key`）と値用の列（接尾辞 `_value`）がそれぞれ 1 つずつ含まれます。| `visit_tallies`<br> `visit_tallies_view`<br> `visitor_tallies`<br> `visitor_tallies_view`<br> `visitor_tallies_view_normalized`|
|**統合された訪問**<br>[訪問の統合]()の一環として、プロファイル内で統合された訪問 ID。| `visitor_replaces`<br> `visitor_replaces_view`|
|**訪問**<br>現在の訪問属性と、その訪問が属するオーディエンス。| `visits`<br> `visits_view`|
|**訪問**<br>訪問属性と、その訪問が属するオーディエンス。| `visitors`<br> `visitors_view`<br> `visitors_view_normalized`|
|**訪問バッチ**|内部使用のみ|

### 訪問テーブル、ビュー、正規化ビュー

AudienceDB は、訪問データをテーブル、ビュー、正規化ビューとして公開します。それぞれ異なる目的で使用されます。

|テーブル／ビュー名|説明|
|---|---|
| `visitors`（テーブル） | 各訪問のすべての履歴行が含まれ、すべての状態変更が記録されます。列名には属性 ID（例：`badge_30`、`flag_5052`）が使用されます。このテーブルは、監査および経時的な変更を確認するクエリに使用します。 |
| `visitors_view`（ビュー） | 最新の状態のみが含まれます（訪問ごとに 1 行）。列名には属性 ID と属性名（例：`visitor - badge - VIP (13)`）が使用されます。このビューは、現在の状態に関するレポートに使用します。 |
| `visitors_view_normalized`（正規化ビュー） | `visitors_view` と同じ行が含まれますが、列名から属性 ID が省略されます（例：`visitor - badge - VIP`）。このビューは、BI ツール、および列名を一定に保つ必要がある安定したダッシュボードで使用します。 |
| `visitor_replaces`（テーブル） | 置き換えられた ID を含む、統合された訪問 ID マッピングのすべてのバージョンが含まれます。このテーブルは、統合の完全な履歴を確認するために使用します。 |
| `visitor_replaces_view`（ビュー） | 置き換えられていない最新の訪問 ID のみが含まれます。このビューは、訪問 ID を現在のプロファイルに解決するために使用します。 |

## データベース構造の例

次のセクションでは、各ビューに固有の特徴と、他のビューとの違いを判断する際に役立つ、各ビューの構造例を示します。

### 訪問配列

次の例は、`visit_arrays` テーブルの基本的な形式を示しています。

```nohl
 visit_id                          | index | updated                 | visit_array_421
 ----------------------------------+--------------------------------------------------------------------------
 13e1a63890793caa346f90607a76c1c98 | 0     | 2018-05-17 01:03:30.344 | Smartphone
 13e1a63890793caa346f90607a76c1c98 | 1     | 2018-05-17 01:03:30.344 | Phone Charger
 13e1a63890793caa346f90607a76c1c98 | 2     | 2018-05-17 01:03:30.344 | Smartphone Case
```

### 訪問リスト

次の例は、`visit_lists` テーブルの基本的な形式を示しています。

```nohl
myexample=# select visit_id, updated, visit_list_284 from visit_lists;

 visit_id                          | updated                 | visit_list_284
 ----------------------------------+-------------------------------------------------------------------------
 13e1a63890793caa346f90607a76c1c98 | 2018-04-22 12:50:20.471 | Cell Phones & Accessories
 13e1a63890793caa346f90607a76c1c98 | 2018-04-22 12:50:20.471 | Computers and Tablets
 13e1a63890793caa346f90607a76c1c98 | 2018-04-22 12:50:20.471 | Office Supplies
```
### 訪問集計

次の例は、`visitor_tallies` テーブルの基本的な形式を示しています。

```nohl
myexample=# select visit_id, updated, visit_tally_5144_key, visit_tally_5144_value from visit_tallies;

                        visit_id                                 | updated                 | visit_tally_5144_key | visit_tally_5144_value
-----------------------------------------------------------------+-------------------------+----------------------+-----------------------
19fd8716d2f8341b81f84f471b5f950873d5c88acee9c61089f286fb8b5d4903 | 2017-09-04 20:39:05.303 | Furniture            | 2
06db172cf2a8fd7f9ff882a28a14ad266ee67824c9bc3ee0b1fcc451b42cec68 | 2017-09-05 06:20:16.209 | Furniture            | 14
162e22ba6c168bff2385bcfba9d4ba8e15767d1ad8b519b3a872a2ad89d3f3dd | 2017-09-05 06:04:59.671 | Search               | 2
4225575ce21a7f9454c56c269eccfee9782e03c6f647a743f058b7b667dd3bbb | 2017-09-20 06:30:14.63  | Home                 | 1
e1e5dd5e58bc97056f8340e242205e1ec2ab0a88c94c890563399f55828638f7 | 2017-09-09 14:22:08.575 | Furniture            | 3
(5 rows)
```

### 訪問配列ビュー

次の例は、`visitor_arrays_view` テーブルの基本的な形式を示しています。

```nohl
myexample=# select "visitor - id", "index", "updated", "visitor array - cart product name (421)" from visitor_arrays_view;

 "visitor array - visitor id"      | index | updated                 | "visitor array - cart product name (421)"
 ----------------------------------+--------------------------------------------------------------------------
 13e1a63890793caa346f90607a76c1c98 | 0     | 2018-05-17 01:03:30.344 | Smartphone
 13e1a63890793caa346f90607a76c1c98 | 1     | 2018-05-17 01:03:30.344 | Phone Charger
 13e1a63890793caa346f90607a76c1c98 | 2     | 2018-05-17 01:03:30.344 | Smartphone Case

```

### 訪問リスト

次の例は、`visitor_lists` テーブルの基本的な形式を示しています。

```nohl
myexample=# select visitor_id, updated, visitor_list_5168 from visitor_lists;

                  visitor_id                   |         updated         | visitor_list_5168
-----------------------------------------------+-------------------------+-------------------
 015e94db670900084e37016b9b7300087002f07f00432 | 2017-11-04 13:30:33.553 | Cell Phones
 015e94db670900084e37016b9b7300087002f07f00432 | 2017-11-04 13:30:33.553 | Phone Accessories
 015e94db670900084e37016b9b7300087002f07f00432 | 2017-11-04 13:30:33.553 | Office Supplies

```

### 訪問置換

次の例は、`visitor_replaces` テーブルの基本的な形式を示しています。

```nohl
myexample=# select visitor_replaces_id, visitor_id, updated from visitor_replaces where updated is not null;

                visitor_replaces_id           | visitor_id                                      | updated
----------------------------------------------+-------------------------------------------------+------------------------
015f8d82498b00132b921ecf890d00089001c08100432 | myexample_main__5216_username@gmail.com         | 2017-11-23 15:32:28.81
015f4a0302b9009e17205a49027005079001c07100c48 | myexample_main__5216_username@myexample.com     | 2017-11-24 22:50:31.105
015feb1537cc00305e319fca622400085001d07d00720 | myexample_main__5216_username@yahoo.com         | 2017-11-26 01:22:27.57
015decf4f3170011afb0979834420007e007b07600720 | myexample_main__5216_username@hotmail.com       | 2018-01-03 22:03:20.837
015e3b903e48000c7944f6af4b8e00087016907f0049e | myexample_main__5216_username@cox.net           | 2018-01-28 03:59:45.031
(5 rows)
```

### 訪問集計

次の例は、`visitor_tallies` テーブルの基本的な形式を示しています。

```nohl
myexample=# select visitor_id, updated, visitor_tally_57_key, visitor_tally_57_value from visitor_tallies;

                 visitor_id                   |         updated         | visitor_tally_57_key | visitor_tally_57_value
----------------------------------------------+-------------------------+----------------------+------------------------
015dcd068996007c1f95a24aa47002075008d06d0093c | 2017-09-01 03:14:18.519 | Safari               |                      8
015e40b27e55004ec842e2b9d0f800090001c08800408 | 2017-09-02 13:35:40.834 | Chrome               |                      2
015e34c9fd270014a6799597769a00088008808000408 | 2017-08-31 05:44:14.013 | Chrome               |                      1
(5 rows)
```

### 訪問ビュー

次の例は、`visitors_view` テーブルの基本的な形式を示しています。

```nohl
select "visitor - id", "visitor - created", "updated", "visitor - audience - bedroom shoppers (myexample_main_102)" from visitors_view limit 1;

                 visitor - id                  |  visitor - created  |        updated         | visitor - audience - bedroom shoppers (myexample_main_102)
-----------------------------------------------+---------------------+------------------------+---------------------------------------------------------------
 015de32cbb1e00265733c8c3c5bc00080001c07800976 | 2017-08-14 23:55:46 | 2017-08-20 15:27:48.75 | f
(1 rows)

```

### 訪問テーブル

次の例は、`visits` テーブルの基本的な形式を示しています。

```nohl
myexample=# select visit_id, visitor_id, start_time, last_event_time, updated, property_5300, flag_5432 from visits limit 5;

                       visit_id                                  | visitor_id                                    |     start_time      | last_event_time     | updated                 | property_5300 | flag_5432
-----------------------------------------------------------------+-----------------------------------------------+---------------------+---------------------+-------------------------+---------------+-----------
4af5f070998b6e471d05a809d55c62811784c57ee196c39a599c0a352e925e01 | 015c9e257f220048ebb26bfdb68405072001c06a00bd0 | 2017-07-18 17:04:31 | 2017-07-18 17:39:27 | 2017-07-18 18:09:28.994 |               |
42fd5d3067b5472a57aa7fe6e8cf12d5d60ea2a9399d54de01bfb0b06e33bd73 | 015cc166a9b100028f7070a6e51d01049003e00d00bd0 | 2017-07-18 21:10:21 | 2017-07-18 21:13:32 | 2017-07-18 21:43:32.948 |               |
9729e709ec80bc476dc6c36c6bf33f998f92c3f2e3af5509078c6402ceff29bf | 015d56a5ec3d00128011a73f446404079001c07100838 | 2017-07-19 18:28:26 | 2017-07-19 18:28:26 | 2017-07-19 18:38:27.903 |               |
6d1c801fb894234347d27a61b9b0f82ac918bfdc36a0510ab3be8ea6a72b9038 | 015c662062aa00474d60cc4f7b4005072001c06a00bd0 | 2017-07-19 19:30:08 | 2017-07-19 19:30:08 | 2017-07-19 19:40:12.802 |               |
c97a0a0c9dfc4cb58e23dbfdb98528cddc8a989c9d65f0e6fd89ffdc5e82c727 | 015c662062aa00474d60cc4f7b4005072001c06a00bd0 | 2017-07-19 21:33:00 | 2017-07-19 21:33:00 | 2017-07-19 21:43:02.803 |               |
(5 rows)
```
## ステッチされた訪問について

AudienceDB では、ステッチされた訪問については、訪問テーブル内で1つの訪問プロファイルのみが維持されます。ステッチされた訪問の訪問プロファイルは、ID は異なるものの、1つのプロファイルとして扱われます。これを実現するため、`visitor_replaces` テーブルでは、置き換えられた `visitor_ids` を参照する方法が提供されています。

Visitor Replaces テーブルの例：

|`visitor_replaces_id`| `visitor_id`|
|---| ---|
|1| 3|
|2| 3|
|4| 6|
|5| 6|

このテーブルでは、次のようになります。

* Visitor1 と Visitor2 は Visitor3 にステッチされています。
* Visitor4 と Visitor5 は Visitor6 にステッチされています。

必要に応じて、上記の情報を使用して `visitors` テーブルを `visits` テーブルまたは EventDB テーブルに結合できます。

EventDB のイベントを AudienceDB に結合するには、次のようにします。

* ステッチされていない訪問については、`events_x` を `visitors` テーブルに直接結合します。
* ステッチされた訪問については、次の例に示すように、`visitor_replaces` テーブルを介して結合します。

```sql
SELECT e."event - id", v."visitor - id"
FROM account__profile.events_view__all_events__all_events e
LEFT JOIN account__profile.visitor_replaces_view r ON e."event - visitor id" = r."visitor - replaces id"
JOIN account__profile.visitors_view_normalized v ON (v."visitor - id" = r."visitor - id" or v."visitor - id" = e."event - visitor id")
limit 1000;
```

* この例では、`events_all_events` 内の訪問 ID が `visitors` または `visitor_replaces` のいずれかに存在する場合を考慮しています。  

<blockquote>
単一イベントのセッションに関連付けられた訪問は、訪問テーブルには保存されません。
</blockquote>


## その他のリソース

* [(Amazon Redshift™) クエリ設計のベストプラクティス](https://docs.aws.amazon.com/redshift/latest/dg/c_designing-queries-best-practices.html)
* [(Amazon Redshift™) クエリパフォーマンスのチューニング](https://docs.aws.amazon.com/redshift/latest/dg/c-optimizing-query-performance.html)