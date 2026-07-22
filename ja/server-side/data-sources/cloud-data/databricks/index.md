---
title: Databricksクラウドデータソース
description: この記事では、Databricksクラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/databricks/
---
クラウドデータソースの構成の一般的な概要については、[manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)を参照してください。

## データタイプ

Databricksデータソースは、すべてのDatabricksデータタイプをサポートしています。データが正しくインポートされるように、以下のガイドラインに従ってDatabricksデータタイプをマッピングしてください：

| Databricks | Tealium |
|:----------|:--------|
| 数値データタイプ  | 数値属性 |
| 文字列およびバイナリデータタイプ | 文字列属性 |
| 論理データタイプ | ブール属性|
| 日付および時間データタイプ| 日付属性 |
| 配列 | 文字列の配列、数値の配列、またはブールの配列|
| マップ、構造体、オブジェクト、バリアント | 文字列属性 |

詳細については、Databricks: データタイプ ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-datatypes), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-datatypes), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-datatypes))を参照してください。

## 接続の作成

Tealiumはサービスプリンシパルを使用してDatabricksの計算リソースにアクセスします。進む前に、Databricksでサービスプリンシパルを作成し、OAuthシークレットを生成する必要があります。詳細については、[Databricks: OAuthを使用してサービスプリンシパルでアクセスを認証する](https://docs.databricks.com/aws/en/dev-tools/auth/oauth-m2m)を参照してください。


<blockquote>
Databricksの個人アクセストークン（PAT）はサポートされていません。詳細については、Databricks: Databricks個人アクセストークンで認証する（レガシー） ([AWS](https://docs.databricks.com/aws/en/dev-tools/auth/pat), [Azure](https://learn.microsoft.com/en-us/azure/databricks/dev-tools/auth/pat), [GCP](https://docs.databricks.com/gcp/en/dev-tools/auth/pat))を参照してください。
</blockquote>


新しい接続を構成するには、次の接続詳細を入力します：

* **ホスト名**: Databricks計算リソースのホスト名。例：
  * AWS: `MY_ACCOUNT.cloud.databricks.com`
  * Azure: `MY_ACCOUNT.azuredatabricks.net`
  * GCP: `MY_ACCOUNT.gcp.databricks.com`
* **HTTPパス**: 計算リソースへのHTTPパス。例：`/sql/1.0/warehouses/3fbc78304284503a`。HTTPパスを見つけるには、Databricksで**SQLウェアハウス**画面に移動し、テーブルが配置されているウェアハウスを選択し、**接続詳細**をクリックします。
* **カタログ**: この接続のカタログ名。
* **スキーマ**: この接続のスキーマ名。
* **OAuthクライアントID**: サービスプリンシパルのUUIDまたはアプリケーションID。
* **OAuthクライアントシークレット**: サービスプリンシパルが生成したシークレット。

詳細については、Databricks: 計算構成 ([AWS](https://docs.databricks.com/aws/en/integrations/jdbc/compute), [Azure](https://learn.microsoft.com/en-us/azure/databricks/integrations/jdbc/compute), [GCP](https://docs.databricks.com/gcp/en/integrations/jdbc/compute))を参照してください。

Databricksに接続した後、**テーブル選択**リストからデータソーステーブルを選択します。

## クエリ構成

一般的な概要については、を参照してください。

Databricksについては、以下の要件に注意してください：

* **タイムスタンプ + インクリメント**および**タイムスタンプ**クエリモード：選択されたタイムスタンプ列は`TIMESTAMP`タイプでなければなりません。
詳細については、Databricks: TIMESTAMPタイプ ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/data-types/timestamp-type), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/data-types/timestamp-type), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/data-types/timestamp-type))を参照してください。
* **インクリメント**クエリモード：選択された数値列は、追加されるたびに値が増加する必要があります。自動インクリメント列の推奨定義は次のとおりです：

```sql
COL1 BIGINT GENERATED ALWAYS AS IDENTITY (START WITH 1 INCREMENT BY 1)
```

詳細については、Databricks `CREATE TABLE` ([AWS](https://docs.databricks.com/aws/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using), [Azure](https://learn.microsoft.com/en-us/azure/databricks/sql/language-manual/sql-ref-syntax-ddl-create-table-using), [GCP](https://docs.databricks.com/gcp/en/sql/language-manual/sql-ref-syntax-ddl-create-table-using))を参照してください。

## IPアクセスリスト

DatabricksワークスペースがIPアドレスによって制限されている場合、[Tealium IPアドレス](https://docs.tealium.com/ip-allow-list/)をDatabricksのIPアクセスリストに追加してください。

詳細については、Databricks: IPアクセスリストの管理 ([AWS](https://docs.databricks.com/aws/en/security/network/front-end/ip-access-list), [Azure](https://learn.microsoft.com/en-us/azure/databricks/security/network/front-end/ip-access-list), [GCP](https://docs.databricks.com/gcp/en/security/network/front-end/ip-access-list))を参照してください。