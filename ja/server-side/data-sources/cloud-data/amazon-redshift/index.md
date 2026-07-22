---
title: Amazon Redshift クラウドデータソース
description: この記事では、Amazon Redshift クラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/amazon-redshift/
---
クラウドデータソースの構成の一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## データタイプ

Amazon Redshift データソースは、すべての Amazon Redshift データタイプをサポートしています。データが正しくインポートされるように、以下のガイドラインに従って Amazon Redshift データタイプをマッピングしてください：

| Amazon Redshift | Tealium |
|:----------|:--------|
| 数値タイプ  | 数値属性 |
| 文字列、マルチバイト文字、SUPER、VARBYTE タイプ| 文字列属性 |
| ブール型 | ブール属性|
| 日付型 | 日付属性 |

詳細については、[Amazon Redshift: データタイプ](https://docs.aws.amazon.com/redshift/latest/dg/c_Supported_data_types.html)を参照してください。

## 接続の作成

Tealium は JDBC を使用して Amazon Redshift に接続します。このプロセスには、クラスターの完全な JDBC URL、ユーザー名、パスワードが必要です。

JDBC URL は次の形式を使用します：  
`jdbc:redshift://hostname:port/database`

新しい接続を構成するには、次の接続詳細を入力します：

* **ホスト名**：Amazon Redshift クラスターのホスト名。例：`examplecluster.abc123xyz789.us-west-2.redshift.amazonaws.com`
* **ポート**：クラスターを起動したときに指定したポート番号。
* **データベース**：接続するデータベース。
* **スキーマ**：接続するスキーマ。

Amazon Redshift に接続した後、**データ選択**リストからテーブルまたはビューを選択します。

詳細については、[Amazon Redshift: JDBC URL の取得](https://docs.aws.amazon.com/redshift/latest/mgmt/jdbc20-obtain-url.html)を参照してください。

## クエリ構成

一般的な概要については、を参照してください。

**タイムスタンプ**を使用するクエリモードでは、選択したタイムスタンプ列は `TIMESTAMP` または `TIMESTAMPTZ` のタイプでなければなりません。

詳細については、[Amazon Redshift: TIMESTAMP](https://docs.aws.amazon.com/redshift/latest/dg/r_Datetime_types.html)を参照してください。

**インクリメント**を使用するクエリモードでは、選択した数値列は整数タイプのいずれかであり、行が追加されるたびに値が増加する必要があります。

詳細については、[Amazon Redshift: 整数タイプ](https://docs.aws.amazon.com/redshift/latest/dg/r_Numeric_types201.html#r_Numeric_types201-integer-types)を参照してください。