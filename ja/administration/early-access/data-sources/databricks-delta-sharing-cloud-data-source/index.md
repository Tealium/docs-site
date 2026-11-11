---
title: Databricks Delta Sharing クラウドデータソース
description: この記事では、Databricks Delta Sharing クラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/administration/early-access/data-sources/databricks-delta-sharing-cloud-data-source/
---

<blockquote>
Databricks Delta Sharing クラウドデータソースは現在早期アクセス段階にあり、一部のお客様のみご利用いただけます。Databricks Delta Sharing の利用を開始するには、Tealium サポートにお問い合わせください。
</blockquote>


クラウドデータソースの構成に関する一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## 仕組み

Databricks Delta Sharing クラウドデータソースでは、Databricks 間共有プロトコルを使用します。このプロトコルにより、Databricks と Tealium の間でデータアセットを安全に共有できます。

このプロトコルでは、お客様がプロバイダー、Tealium が受信者となります。Databricks で共有を作成し、その共有へのアクセス権を Tealium に付与します。共有とは、読み取り専用のテーブルとアセットのコレクションです。

Tealium 共有識別子（メタストア ID）を使用して、Databricks で Tealium への安全な接続を構成します。データベースのユーザー名、パスワード、アクセストークンが Databricks の外部に送信されることはありません。

[Data Cloud Activation](https://docs.tealium.com/about-data-cloud-activation/) と併用する場合、データパイプラインはゼロコピーになります。データは Databricks 環境内に保持され、アクティベーション時にオンデマンドでアクセスされます。

## データ型

Databricks Delta Sharing データソースは、Databricks のすべてのデータ型をサポートしています。データが正しくインポートされるように、次のガイドラインに従って Databricks のデータ型をマッピングしてください。

| Databricks | Tealium |
|:----------|:--------|
| 数値データ型 | Number 属性 |
| 文字列およびバイナリデータ型 | String 属性 |
| 論理データ型 | Boolean 属性 |
| 日付および時刻データ型 | Date 属性 |
| 配列 | 文字列の配列、数値の配列、またはブール値の配列 |
| Map、struct、object、variant | String 属性 |

詳細については、Databricks：データ型（[AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-datatypes)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-datatypes)、[GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-datatypes)）を参照してください。

## 接続の作成


<blockquote>
Delta Sharing を構成するには、ユーザーに Databricks Unity Catalog の次の権限が必要です：`CREATE RECIPIENT`、`CREATE SHARE`、`USE CATALOG`、`USE SCHEMA`、`SELECT`。メタストア管理者には、これらの権限がすでに付与されています。
</blockquote>


Databricks Delta Sharing との接続を作成するには、Databricks で次の手順を実行します。

1. 共有するデータが含まれている Databricks Unity Catalog メタストアで Delta Sharing を有効にします。  
詳細については、Databricks：メタストアで Delta Sharing を有効にする（[AWS](https://docs.databricks.com/aws/en/delta-sharing/set-up#enable)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/set-up#enable)、[GCP](https://docs.databricks.com/gcp/en/delta-sharing/set-up#enable)）を参照してください。
1. Tealium と共有するテーブル、ビュー、またはカタログを含む共有を作成します。  
詳細については、Databricks：Delta Sharing の共有を作成および管理する（[AWS](https://docs.databricks.com/aws/en/delta-sharing/create-share)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/create-share)、[GCP](https://docs.databricks.com/gcp/en/delta-sharing/create-share)）を参照してください。
1. 受信者を作成します。Tealium 受信者の作成に必要な `metastore_id` については、Tealium サポートにお問い合わせください。  
詳細については、Databricks：Delta Sharing のデータ受信者を作成および管理する（Databricks 間共有）（[AWS](https://docs.databricks.com/aws/en/delta-sharing/create-recipient)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/create-recipient)、[GCP](https://docs.databricks.com/gcp/en/delta-sharing/create-recipient)）を参照してください。
1. 1 つ以上の共有へのアクセス権を Tealium に付与します。  
詳細については、Databricks：Delta Sharing データ共有へのアクセスを管理する（プロバイダー向け）（[AWS](https://docs.databricks.com/aws/en/delta-sharing/grant-access)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/delta-sharing/grant-access)、[GCP](https://docs.databricks.com/gcp/en/delta-sharing/grant-access)）を参照してください。
1. 接続の作成を Tealium サポートに依頼します。接続を作成するために、Tealium サポートにはお客様の Databricks Workspace 名が必要です。

Tealium で Databricks Delta Sharing クラウドデータソースを作成するには、次の手順を実行します。

1. Tealium サポートがお客様向けの接続を作成した後、Tealium で Databricks Delta Sharing クラウドデータソースを作成します。詳細については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。
1. **接続を確立**をクリックします。Databricks への Delta Sharing 接続の確立には、最長で 2～3 分かかる場合があります。

## クエリ構成

一般的な概要については、を参照してください。

Databricks Delta Sharing では、次の要件に注意してください。

* **Timestamp + Incrementing** および **Timestamp** クエリモード：選択するタイムスタンプ列の型は `TIMESTAMP` である必要があります。  
詳細については、Databricks：TIMESTAMP 型（[AWS](https://docs.databricks.com/aws/en/sql/language-manual/data-types/timestamp-type)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/data-types/timestamp-type)、[GCP](https://docs.databricks.com/gcp/en/sql/language-manual/data-types/timestamp-type)）を参照してください。
* **Incrementing** クエリモード：選択する数値列の値は、行が追加されるたびに増加する必要があります。自動インクリメント列には、次の定義を推奨します。

```sql
COL1 BIGINT GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1)
```

詳細については、Databricks の `CREATE TABLE`（[AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-ddl-create-table-using)、[GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using)）を参照してください。

## IP アクセスリスト

Databricks Workspace が IP アドレスによって制限されている場合は、[Tealium の IP アドレス](https://docs.tealium.com/ip-allow-list/)を Databricks の IP アクセスリストに追加してください。

詳細については、Databricks：IP アクセスリストを管理する（[AWS](https://docs.databricks.com/aws/en/security/network/front-end/ip-access-list)、[Azure](https://learn.microsoft.com/en-us/azure/databricks/security/network/front-end/ip-access-list)、[GCP](https://docs.databricks.com/gcp/en/security/network/front-end/ip-access-list)）を参照してください。