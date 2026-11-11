---
title: Context API と Data Cloud Activation の統合ガイド
description: Data Cloud Activation セグメントからリアルタイムの訪問データを取得するように Context API を構成します。
url: https://docs.tealium.com/ja/administration/early-access/context-api/context-api-data-cloud-activation-integration/
---
## 仕組み

Context API は Data Cloud Activation との直接統合をサポートしており、データクラウドから直接取得したデータを使用して、リアルタイムのパーソナライゼーションを作成できます。Snowflake や Databricks などのクラウドデータソースに基づいて、Data Cloud Activation セグメントから訪問データを取得します。

この統合により、データクラウドとリアルタイム API レスポンスの間に橋渡しが構築されます。これにより、データウェアハウスのスケーラビリティと Context API の低レイテンシ性能を組み合わせたパーソナライゼーションが可能になります。

この統合には、Data Cloud Activation プロファイルと Context API の両方での構成が必要です。

## 前提条件

* 1 つ以上のクラウドデータソースが構成された Data Cloud Activation プロファイル
* クラウド属性を使用して作成された Data Cloud Activation セグメント
* アカウントで Context API が有効になっていること

## 手順 1：クラウドデータソースを構成する

Data Cloud Activation プロファイルで、Context API とともに使用する各クラウドデータソースに対して Context API 統合を構成します。

1. Data Cloud Activation プロファイルで、**Connect > Data Sources** に移動します。
1. 新しいクラウドデータソースを作成するか、既存のデータソースを編集します。
1. データソース構成の **Context API Integration** セクションに移動します。
1. **Context API Integration** を有効にします。
1. 各レコードの一意の識別子を含むクラウドデータソースの列を選択します。
    * この識別子は、訪問またはエンティティごとに一意である必要があります（訪問 ID、顧客 ID、メールアドレスなど）。
    * 文字列または数値のデータ型を持つ列のみがサポートされます。
    * この列の値は、Context API エンドポイントの `momentsApiId` パラメータに使用されます。
1. データソースの残りの構成を完了し、変更を保存します。

これで、クラウドデータソースを Context API エンジンのソースとして使用できるようになります。

## 手順 2：Data Cloud Activation セグメントを作成する

Context API を介して利用可能にするオーディエンスを定義するセグメントを、Data Cloud Activation プロファイルで作成します。

1. Data Cloud Activation プロファイルで **Audience** に移動します。
1. データソースのクラウド属性を使用してセグメントを作成します。
1. Context API で使用するセグメントを保存して有効にします。

これらのセグメントは、Context API エンジンを構成するときに選択できるようになります。

## 手順 3：Context API エンジンを構成する

Context API の構成で、API レスポンスに含める Data Cloud Activation のデータソースとセグメントを追加します。

1. Data Cloud Activation プロファイルで、**CloudStream > Context API** に移動します。
1. 新しいエンジンを作成するか、既存のエンジンを編集します。
1. **Details** 画面で、エンジン名、有効化ステータス、ドメイン許可リストを構成します。
1. **Next** をクリックします。
1. **Cloud Data Source** 画面で、次の操作を行います。
    * **Add Data Source** をクリックして、クラウドデータソースを追加します。
    * 追加したクラウドデータソースごとに、エンジン構成で使用する Data Cloud Activation セグメントを選択します。
    * 選択したすべてのセグメントのレコードが、エンジン構成に事前入力されます。
1. **Next** をクリックします。
1. **Response** 画面で、Data Cloud Activation セグメントが **Example Response** にオーディエンスとして表示されていることを確認します。
    * 必要に応じて、追加の Data Cloud Activation 属性を選択できます。サポートされるデータ型は、数値、文字列、ブール値、日付です。
    * レスポンスペイロードの属性に ID と名前のどちらを使用するかを選択します。
1. **Example Response** パネルを確認し、構成が正しいことを検証します。
1. **Next** をクリックし、エンジンの概要を確認します。
1. **Done** をクリックしてエンジンを保存します。

## 手順 4：Context API エンドポイントを呼び出す

`momentsApiId` パラメータを使用して、Data Cloud Activation セグメントから訪問データを取得します。

### Context API エンドポイント

```bash
GET https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{momentsApiId}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

### パラメータ

| **パラメータ** | **型** | **説明** |
|---|---|---|
| `momentsApiId` | 文字列<br>パスパラメータ | クラウドデータソースの Context API Integration で構成されたクラウド属性の値。これは、手順 1 で選択した列の属性値です。特殊文字はエンコードする必要があります。 |
| `suppressNotFound` | ブール値<br>クエリパラメータ | 訪問が見つからない場合のレスポンス形式を指定します。デフォルトは `false` です。<br>`true` - 空のレスポンスボディとともに HTTP 200 を返します。<br>`false` - HTTP 404 を返します。 |

### リクエストの例

```bash
GET https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example-account/profiles/cloudstream-profile/engines/abc123/visitors/user%40example.com?suppressNotFound=true
```

この例では、次のようになります。

* `user%40example.com` は、クラウドデータソース構成でマッピングされたクラウド属性の値です。

### レスポンス形式

レスポンスは標準の Context API レスポンス形式に従い、Data Cloud Activation セグメントのオーディエンスが含まれます。

```json
{
    "audiences": [
        "30 Days Since Last Login"
    ],
    "metrics": {
        "Total direct visits": 1
    },
    "properties": {
        "Company Name": "<attr_value>"
    },
    "flags": {
        "Returning visitor": false
    },
    "dates": {
        "First visit": 1491233145706
    }
}
```

## ベストプラクティス

* **安定した識別子を選択する**：セッションをまたいで維持される、安定した一意の識別子（顧客 ID やメールアドレスのハッシュなど）を含む列を選択します。
* **suppressNotFound を使用してテストする**：テスト中は、`suppressNotFound=true` を使用して、データソースに存在しない訪問に対する HTTP 404 レスポンスを回避します。
* **セグメントのメンバーシップを監視する**：Context API レスポンスに含まれることを想定している訪問層を取得できるよう、Data Cloud Activation セグメントが構成されていることを確認します。
* **更新を調整する**：クラウドデータソース構成の変更は、Context API レスポンスに影響する可能性があります。両方のシステムにまたがる更新を調整してください。

## 関連ドキュメント

* [about-data-cloud-activation](https://docs.tealium.com/about-data-cloud-activation/)
* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)
* [about-context-api](https://docs.tealium.com/about-context-api/)
* [context-api-endpoint](https://docs.tealium.com/context-api-endpoint/)
* [context-api-manage-engines](https://docs.tealium.com/context-api-manage-engines/)