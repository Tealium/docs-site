---
title: Google BigQuery クラウドデータソース
description: この記事では、Google BigQuery クラウドデータソースの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side/data-sources/cloud-data/google-bigquery-cloud-data-source/
---クラウドデータソースの構成に関する一般的な概要については、を参照してください。

## データタイプ

Google BigQuery データソースは、Google BigQuery のすべてのデータタイプをサポートしています。データが正しくインポートされるように、以下のガイドラインに従って Google BigQuery データタイプをマッピングしてください：

| Google BigQuery | Tealium |
|:----------------|:--------|
| 数値データタイプ  | 数値属性 |
| 文字列およびバイナリデータタイプ | 文字列属性 |
| 論理データタイプ | ブール属性|
| 日付および時間データタイプ| 日付属性 |
| 配列 | 文字列の配列、数値の配列、またはブールの配列|
| JSON | 文字列属性 |
| STRUCT | [STRUCT列のインポート](#importing-struct-columns)を参照してください。

詳細については、[Google BigQuery: データタイプ](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types)を参照してください。

## 接続の作成

TealiumはOAuth 2.0フローを使用してGoogleと認証します。このプロセスには、サービスアカウントとプライベートキーファイルが必要です。

サービスアカウントには、以下のBigQuery IAMロールが必要です：

* [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer)
* [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser)

公開/秘密キーペアを生成するには：

1. **Google Cloud &gt; サービスアカウント**に移動し、プロジェクトを選択するか、新しく作成します。
1. サービスアカウントを選択するか、新しく作成し、**キー**タブに移動して**キーの追加 &gt; 新しいキーの作成**を選択します。
1. **JSON**オプションを選択し、**作成**をクリックします。  
プライベートキーが生成され、マシンにダウンロードされます。

新しい接続を構成するには、次の接続詳細を入力します：

* **データセット**: 指定されたプロジェクト内のデータセットの名前。プロジェクト名は含めません。
* **プロジェクトID**: Google CloudプロジェクトのプロジェクトID。
* **サービスアカウントのメールアドレス**: サービスアカウントの生成されたメールアドレス。
* **キーファイル**: サービスアカウント用に生成されたプライベートキーファイルをアップロードするか、以前にアップロードされたキーファイルを選択します。

Google BigQueryに接続した後、**データ選択**リストからテーブルまたはビューを選択します。

詳細については、[Google for Developers: サーバー間アプリケーション用のOAuth 2.0の使用](https://developers.google.com/identity/protocols/oauth2/service-account#creatinganaccount)を参照してください。

## クエリバッチサイズ

デフォルトのクエリバッチサイズは、バッチあたり1,000レコードです。デフォルトからクエリバッチサイズを変更するには追加の権限が必要になる場合があります。クエリサイズ制限を変更する権限を付与するには、**Google Cloudコンソール &gt; IAMメニュー &gt; 適切なサービスアカウントを選択 &gt; アクセスを許可 &gt; BigQuery Read Session User Roleを追加**します。たとえば、`BigQuery Read Session User (roles/bigquery.readSessionUser)`を入力します。詳細については、[Google: BigQuery IAMロールと権限](https://docs.cloud.google.com/bigquery/docs/access-control)およびを参照してください。

## クエリ構成

一般的な概要については、を参照してください。

クエリモードが**Timestamp**を使用する場合、選択されたタイムスタンプ列は`TIMESTAMP`タイプでなければなりません。

詳細については、[Google BigQuery: TIMESTAMP](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#timestamp_type)を参照してください。

クエリモードが**Incrementing**を使用する場合、選択された数値列は、追加される各行に対して値が増加する必要があります。`FLOAT`や`DECIMAL`ではなく、`INT64`のような整数タイプを使用してください。

詳細については、[Google BigQuery: 数値タイプ](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_types)を参照してください。

### STRUCT列のインポート

BigQueryの`STRUCT`列はTealiumに直接インポートすることはできません。`STRUCT`列からデータをインポートするには、`STRUCT`フィールドを個別の列にフラット化するビューを作成します。

たとえば、次のように`STRUCT`で定義された住所があるかもしれません：

```sql
shipping_address STRUCT&lt;
  street STRING,
  city STRING,
  state STRING,
  postal_code STRING,
  country STRING
&gt;
```

これらの住所フィールドを個別の列にフラット化するビューを作成するには、次のようなSQLステートメントを使用します：

```sql
CREATE OR REPLACE VIEW ecommerce.order_shipping_view AS
SELECT
  order_id,
  customer_id,
  shipping_address.country AS country,
  shipping_address.postal_code AS postal_code
FROM
  ecommerce.orders;  
```

フラット化された`STRUCT`列は、他のサポートされているデータタイプのようにインポートしてマッピングすることができます。