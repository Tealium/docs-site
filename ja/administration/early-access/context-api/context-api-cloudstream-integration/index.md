---
title: Context APIとCloudStreamの統合ガイド
description: Context APIを構成して、CloudStreamセグメントからリアルタイムの訪問データを取得します。
url: https://docs.tealium.com/ja/administration/early-access/context-api/context-api-cloudstream-integration/
---
## 動作原理

Context APIはCloudStreamとの直接統合をサポートしており、データクラウドから直接データを使用してリアルタイムのパーソナライゼーションを作成できます。SnowflakeやDatabricksなどのクラウドデータソースを基にしたCloudStreamセグメントから訪問データを取得します。

この統合は、データクラウドとリアルタイムAPIレスポンスの間に橋をかけ、データウェアハウスのスケールとContext APIの低遅延パフォーマンスを組み合わせたパーソナライゼーションシナリオを実現します。

統合には、CloudStreamプロファイルとContext APIの両方で構成が必要です。

## 前提条件

* 少なくとも1つのクラウドデータソースが構成されたCloudStreamプロファイル
* クラウド属性を使用して作成されたCloudStreamセグメント
* アカウントで有効になっているContext API

## ステップ1: クラウドデータソースの構成

CloudStreamプロファイルで、Context APIと連携する各クラウドデータソースを構成します：

1. CloudStreamプロファイルで**接続 > データソース**に移動します。
1. 新しいクラウドデータソースを作成するか、既存のものを編集します。
1. データソース構成の**Context API統合**セクションに移動します。
1. **Context API統合**を有効にします。
1. 各レコードに対して一意の識別子を含むクラウドデータソースの列を選択します。
    * この識別子は訪問またはエンティティごとに一意である必要があります（例：訪問ID、顧客ID、またはメールアドレス）。
    * 文字列または数値データ型の列のみがサポートされています。
    * この列の値はContext APIエンドポイントの`momentsApiId`パラメーターで使用されます。
1. データソース構成の残りの部分を完了して変更を保存します。

クラウドデータソースは、Context APIエンジンのソースとして利用可能になりました。

## ステップ2: CloudStreamセグメントの作成

Context APIを通じて利用可能にしたいオーディエンスを定義するCloudStreamセグメントを作成します：

1. CloudStreamプロファイルで**オーディエンス**に移動します。
1. データソースのクラウド属性を使用してセグメントを作成します。
1. Context APIで使用したいセグメントを保存して有効にします。

これらのセグメントは、Context APIエンジンを構成する際に選択可能です。

## ステップ3: Context APIエンジンの構成

Context API構成で、APIレスポンスに含めたいCloudStreamデータソースとセグメントを追加します：

1. CloudStreamプロファイルで**CloudStream > Context API**に移動します。
1. 新しいエンジンを作成するか、既存のものを編集します。
1. **詳細**画面で、エンジン名、有効状態、ドメイン許可リストを構成します。
1. **次へ**をクリックします。
1. **クラウドデータソース**画面で：
    * **データソースを追加**をクリックしてクラウドデータソースを追加します。
    * 追加する各クラウドデータソースについて、エンジン構成で使用するCloudStreamセグメントを選択します。
    * 選択したすべてのセグメントのレコードがエンジン構成に事前に構成されます。
1. **次へ**をクリックします。
1. **レスポンス**画面で、CloudStreamセグメントが**例示レスポンス**のオーディエンスとして表示されることを確認します。
    * 必要に応じて追加のCloudStream属性を選択できます。サポートされるデータタイプ：数値、文字列、ブール値、日付。
    * レスポンスペイロードの属性でIDまたは名前を使用するか選択します。
1. **例示レスポンス**パネルを確認して構成を確認します。
1. **次へ**をクリックし、エンジンの概要を確認します。
1. **完了**をクリックしてエンジンを保存します。

## ステップ4: Context APIエンドポイントの呼び出し

`momentsApiId`パラメータを使用してCloudStreamセグメントから訪問データを取得します。

### Context APIエンドポイント

```bash
GET https://personalization-api.{REGION}.prod.tealiumapis.com/personalization/accounts/{ACCOUNT}/profiles/{PROFILE}/engines/{ENGINE_ID}/visitors/{momentsApiId}?suppressNotFound={SUPPRESS_NOT_FOUND}
```

### パラメータ

| **パラメータ** | **タイプ** | **説明** |
|---|---|---|
| `momentsApiId` | String<br>パスパラメータ | クラウドデータソースのContext API統合で構成されたクラウド属性の値です。これはステップ1で選択した列の属性の値です。特殊文字はエンコードする必要があります。
|
| `suppressNotFound` | Boolean<br>クエリパラメータ | 訪問が見つからない場合のレスポンスタイプを決定します。デフォルトは`false`です。<br> `true` - HTTP 200で空のレスポンスボディを返します。<br> `false` - HTTP 404を返します。 |

### 例示リクエスト

```bash
GET https://personalization-api.us-west.prod.tealiumapis.com/personalization/accounts/example-account/profiles/cloudstream-profile/engines/abc123/visitors/user%40example.com?suppressNotFound=true
```

この例では：
* `user%40example.com`はクラウドデータソース構成でマッピングされたクラウド属性の値です。

### レスポンス形式

レスポンスは標準のContext APIレスポンス形式に従い、CloudStreamセグメントのオーディエンスが含まれます：

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
* **セグメントメンバーシップを監視する**：Context APIレスポンスで期待する訪問集団を捉えるようにCloudStreamセグメントが構成されていることを確認します。
* **更新を調整する**：クラウドデータソースの構成変更がContext APIレスポンスに影響を与える可能性があります。両システム間で更新を調整します。

## 関連ドキュメント

* [about-cloudstream](https://docs.tealium.com/about-cloudstream/)
* [about-cloud-data-sources](https://docs.tealium.com/about-cloud-data-sources/)
* [manage-cloud-data-source](https://docs.tealium.com/manage-cloud-data-source/)
* [about-context-api](https://docs.tealium.com/about-context-api/)
* [context-api-endpoint](https://docs.tealium.com/context-api-endpoint/)
* [context-api-manage-engines](https://docs.tealium.com/context-api-manage-engines/)