---
title: Moments APIとCloudStreamの統合ガイド
description: Moments APIを構成して、CloudStreamセグメントからリアルタイムの訪問データを取得します。
url: https://docs.tealium.com/ja/administration/early-access/moments-api/moments-api-cloudstream-integration/
---
## 動作原理

Moments APIはCloudStreamとの直接統合をサポートしており、データクラウドから直接データを使用してリアルタイムのパーソナライゼーションを作成できます。SnowflakeやDatabricksなどのクラウドデータソースを基にしたCloudStreamセグメントから訪問データを取得します。

この統合は、データクラウドとリアルタイムAPIレスポンスの間に橋をかけ、データウェアハウスのスケールとMoments APIの低遅延パフォーマンスを組み合わせたパーソナライゼーションシナリオを実現します。

統合には、CloudStreamプロファイルとMoments APIの両方での構成が必要です。

## 前提条件

* 少なくとも1つのクラウドデータソースが構成されたCloudStreamプロファイル
* クラウド属性を使用して作成されたCloudStreamセグメント
* アカウントでMoments APIが有効になっていること

## ステップ1: クラウドデータソースの構成

CloudStreamプロファイルで、Moments APIと連携する各クラウドデータソースを構成します：

1. CloudStreamプロファイルの**Connect > Data Sources**に移動します。
1. 新しいクラウドデータソースを作成するか、既存のものを編集します。
1. データソース構成の**Moments API Integration**セクションに移動します。
1. **Moments API Integration**を有効にします。
1. 各レコードに対して一意の識別子を含むクラウドデータソースの列を選択します。
    * この識別子は訪問やエンティティごとに一意である必要があります（例：訪問ID、顧客ID、またはメールアドレス）。
    * 文字列または数値データ型の列のみがサポートされています。
    * この列の値はMoments APIエンドポイントの`momentsApiId`パラメーターに使用されます。
1. データソース構成を完了して変更を保存します。

クラウドデータソースは、Moments APIエンジンのソースとして利用可能になりました。

## ステップ2: CloudStreamセグメントの作成

Moments APIを通じて利用可能にしたいオーディエンスを定義するCloudStreamプロファイルでセグメントを作成します：

1. CloudStreamプロファイルの**Audience**に移動します。
1. データソースのクラウド属性を使用してセグメントを作成します。
1. Moments APIで使用するセグメントを保存して有効にします。

これらのセグメントは、Moments APIエンジンを構成する際に選択可能です。

## ステップ3: Moments APIエンジンの構成

Moments API構成で、APIレスポンスに含めたいCloudStreamデータソースとセグメントを追加します：

1. CloudStreamプロファイルの**CloudStream > Moments API**に移動します。
1. 新しいエンジンを作成するか、既存のものを編集します。
1. **Details**画面で、エンジン名、有効状態、ドメイン許可リストを構成します。
1. **Next**をクリックします。
1. **Cloud Data Source**画面で：
    * **Add Data Source**をクリックしてクラウドデータソースを追加します。
    * 追加する各クラウドデータソースについて、エンジン構成で使用するCloudStreamセグメントを選択します。
    * 選択したすべてのセグメントのレコードがエンジン構成に事前に構成されます。
1. **Next**をクリックします。
1. **Response**画面で、CloudStreamセグメントが**Example Response**のオーディエンスとして表示されることを確認します。
    * 必要に応じて追加のCloudStream属性を選択できます。サポートされるデータタイプ：数値、文字列、ブール値、日付。
    * レスポンスペイロードの属性でIDまたは名前を使用するか選択します。
1. **Example Response**パネルを確認して構成を確認します。
1. **Next**をクリックし、エンジンの概要を確認します。
1. **Done**をクリックしてエンジンを保存します。

## ステップ4: Moments APIエンドポイントの呼び出し

Moments API IDパラメータを使用して、CloudStreamセグメントから訪問データを取得します。

### Moments APIエンドポイント

```bash
GET https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{momentsApiId}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

### パラメータ

| **パラメータ** | **タイプ** | **説明** |
|---|---|---|
| `momentsApiId` | String<br>Path parameter | クラウドデータソースのMoments API統合で構成されたクラウド属性の値。これはステップ1で選択した列の属性の値です。特殊文字はエンコードする必要があります。
|
| `suppressNotFound` | Boolean<br>Query parameter | 訪問が見つからない場合のレスポンスタイプを決定します。デフォルトは`false`です。<br> `true` - HTTP 200で空のレスポンスボディを返します。<br> `false` - HTTP 404を返します。 |

### 例のリクエスト

```bash
GET https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example-account/profiles/cloudstream-profile/engines/abc123/visitors/user%40example.com?suppressNotFound=true
```

この例では：
* `user%40example.com`はクラウドデータソース構成でマッピングされたクラウド属性の値です。

### レスポンス形式

レスポンスは標準のMoments APIレスポンス形式に従い、CloudStreamセグメントのオーディエンスが含まれます：

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

* **安定した識別子を選択する**：セッション間で持続する安定した、一意の識別子を含む列を選択します（例：顧客IDまたはメールハッシュ）。
* **suppressNotFoundでテストする**：テスト中は`suppressNotFound=true`を使用して、データソースに訪問が見つからない場合のHTTP 404レスポンスを避けます。
* **セグメントメンバーシップを監視する**：Moments APIレスポンスで期待する訪問集団を捉えるようにCloudStreamセグメントが構成されていることを確認します。
* **更新を調整する**：クラウドデータソースの構成変更がMoments APIレスポンスに影響を与える可能性があります。両システム間で更新を調整します。

## 関連ドキュメント

* [about-cloudstream](https://docs.tealium.com/about-cloudstream/)
* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)
* [about-moments-api](https://docs.tealium.com/about-moments-api/)
* [moments-api-endpoint](https://docs.tealium.com/moments-api-endpoint/)
* [moments-api-manage-engines](https://docs.tealium.com/moments-api-manage-engines/)