---
title: Databricks Delta Sharing クラウドデータソース
description: この記事では、Databricks Delta Sharing クラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/data-sources/databricks-delta-sharing-cloud-data-source/
---

<blockquote>
Databricks Delta Sharing クラウドデータソースは現在アーリーアクセス中で、選ばれた顧客のみが利用可能です。Databricks Delta Sharing を始めるには、Tealium サポートに連絡してください。
</blockquote>


クラウドデータソースの構成の一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## 動作原理

Databricks Delta Sharing クラウドデータソースは、Databricks 間でデータ資産を安全に共有する Databricks-to-Databricks 共有プロトコルを使用します。

このプロトコルでは、あなたが提供者であり、Tealium が受信者です。Databricks で共有を作成し、それらの共有に対して Tealium へのアクセスを許可します。共有は読み取り専用のテーブルや資産のコレクションです。

Databricks で Tealium 共有識別子（メタストア ID）を使用して Tealium への安全な接続を構成します。データベースのユーザー名、パスワード、またはアクセストークンは Databricks を離れることはありません。

[CloudStream](https://docs.tealium.com/about-cloudstream/) と一緒に使用すると、データパイプラインはゼロコピーです。データはあなたの Databricks 環境内に留まり、オンデマンドでアクティベーションのためにアクセスされます。

## データタイプ

Databricks Delta Sharing データソースは、すべての Databricks データタイプをサポートしています。データが正しくインポートされるように、以下のガイドラインに従って Databricks データタイプをマッピングしてください：

| Databricks | Tealium |
|:----------|:--------|
| 数値データタイプ  | 数値属性 |
| 文字列およびバイナリデータタイプ | 文字列属性 |
| 論理データタイプ | ブール属性|
| 日付および時間データタイプ| 日付属性 |
| 配列 | 文字列の配列、数値の配列、またはブールの配列|
| マップ、構造体、オブジェクト、バリアント | 文字列属性 |

詳細については、Databricks: データタイプ ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-datatypes), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-datatypes), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-datatypes)) を参照してください。

## 接続の作成


<blockquote>
Delta Sharing を構成するためには、ユーザーは次の Databricks Unity Catalog の権限が必要です：`CREATE RECIPIENT`, `CREATE SHARE`, `USE CATALOG`, `USE SCHEMA`, および `SELECT`。メタストア管理者はこれらの権限を既に持っています。
</blockquote>


Databricks Delta Sharing との接続を作成するには、Databricks で次の手順を完了してください：

1. データを共有したいメタストアが含まれている Databricks Unity Catalog で Delta Sharing を有効にします。  
詳細については、Databricks: メタストアで Delta Sharing を有効にする ([AWS](https://docs.databricks.com/aws/en/delta-sharing/set-up#enable), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/set-up#enable), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/set-up#enable)) を参照してください。
1. Tealium と共有する予定のテーブル、ビュー、またはカタログで共有を作成します。  
詳細については、Databricks: Delta Sharing 用の共有の作成と管理 ([AWS](https://docs.databricks.com/aws/en/delta-sharing/create-share), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/create-share), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/create-share)) を参照してください。
1. 受信者を作成します。Tealium 受信者を作成するために必要な `metastore_id` を取得するには、Tealium サポートに連絡してください。  
詳細については、Databricks: Delta Sharing のためのデータ受信者の作成と管理 (Databricks-to-Databricks 共有) ([AWS](https://docs.databricks.com/aws/en/delta-sharing/create-recipient), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/create-recipient), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/create-recipient)) を参照してください。
1. Tealium に1つ以上の共有へのアクセスを許可します。  
詳細については、Databricks: Delta Sharing データ共有へのアクセスの管理 (提供者用) ([AWS](https://docs.databricks.com/aws/en/delta-sharing/grant-access), [Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/grant-access), [GCP](https://docs.databricks.com/gcp/en/delta-sharing/grant-access)) を参照してください。
1. Tealium サポートに連絡して、接続を作成してもらいます。接続を作成するためには、Tealium サポートがあなたの Databricks ワークスペース名を必要とします。

Tealium で Databricks Delta Sharing クラウドデータソースを作成するための次の手順を完了してください：

1. Tealium サポートが接続を作成した後、Tealium で Databricks Delta Sharing クラウドデータソースを作成します。詳細については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。
1. **接続の確立**をクリックします。Databricks への Delta Sharing 接続の確立には最大で2-3分かかる場合があります。

## クエリ構成

一般的な概要については、を参照してください。

Databricks Delta Sharing の場合、以下の要件に注意してください：

* **タイムスタンプ + インクリメント**および**タイムスタンプ**クエリモード：選択されたタイムスタンプ列は `TIMESTAMP` タイプでなければなりません。  
詳細については、Databricks: TIMESTAMP タイプ ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/data-types/timestamp-type), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/data-types/timestamp-type), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/data-types/timestamp-type)) を参照してください。
* **インクリメント**クエリモード：選択された数値列は、追加される各行に対して値が増加する必要があります。自動インクリメント列の推奨定義は次のとおりです：

```sql
COL1 BIGINT GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1)
```

詳細については、Databricks `CREATE TABLE` ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-ddl-create-table-using), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using)) を参照してください。

## IP アクセスリスト

あなたの Databricks ワークスペースが IP アドレスによって制限されている場合、[Tealium IP アドレス](https://docs.tealium.com/ip-allow-list/) を Databricks の IP アクセスリストに追加してください。

詳細については、Databricks: IP アクセスリストの管理 ([AWS](https://docs.databricks.com/aws/en/security/network/front-end/ip-access-list), [Azure](https://learn.microsoft.com/en-us/azure/databricks/security/network/front-end/ip-access-list), [GCP](https://docs.databricks.com/gcp/en/security/network/front-end/ip-access-list)) を参照してください。
