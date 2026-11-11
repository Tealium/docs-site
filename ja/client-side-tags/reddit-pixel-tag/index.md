---
title: Reddit Pixelタグ構成ガイド
description: 広告閲覧後のインタラクションの追跡、コンバージョンの測定、Tag Managementでのリターゲティングの有効化を行うために、Reddit Pixelタグを構成します。
url: https://docs.tealium.com/ja/client-side-tags/reddit-pixel-tag/
---
Reddit Pixelタグは、広告閲覧後のインタラクションを追跡し、コンバージョン測定とリターゲティングをサポートします。

## 要件

* Reddit Adsアカウント
* Reddit Pixel ID

## タグに関するヒント

* マッピングを使用して、標準の構成値を上書きし、イベントをトリガーします。
* **Order ID**が構成されている場合、購入イベントが発生します。
* Reddit PixelのイベントIDをサーバーサイド属性として使用できるようにするには、**Generate Event ID**を`true`に構成し、最新バージョンの[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)を使用します。
* [Reddit Conversionsコネクタ](https://docs.tealium.com/reddit-conversions-connector/)のコンバージョンID構成は、Reddit PixelタグとReddit Conversionsコネクタの両方を実装する場合にのみ使用することをお勧めします。コンバージョンIDを構成すると、同じコンバージョンイベントが両方のソースから送信された場合に二重にカウントされるのを防止できます。この値が不適切に渡されると、アトリビューションとキャンペーンのパフォーマンスに影響します。
* Redditでコンバージョンの追跡とレポートを最も正確に行うために、高度なマッチングを使用することをお勧めします。メールアドレスと電話番号は、プレーン値またはSHA256で事前にハッシュ化した値として渡します。Redditライブラリは、送信前にプレーンなメールアドレスへSHA256ハッシュを適用します。
* 使用するパラメータのみをマッピングし、Redditのドキュメントでサポート状況を確認してください。
* イベントごとに異なるメタデータが必要な場合は、きめ細かな制御を行うためにイベント固有のパラメータを使用します。
* 収益イベントでは、イベントレベルの`value`と`itemCount`、および商品レベルの`quantity`と`itemPrice`の両方を送信します。いずれか一方のフィールドセットのみを送信すると、Reddit Adsでのレポートまたは最適化が制限される可能性があります。
* 商品配列はインデックスの対応関係を維持してください。単一商品のペイロードを意図している場合を除き、単一値と配列を混在させないでください。
* 購入専用のメタデータが誤って他のイベントに適用されないように、イベント固有のパラメータを使用します。
* このタグは、Redditのイベントレベルのパラメータ要件を適用します。未定義または空の値は削除され、特定のイベントについてRedditがサポートしていないパラメータはペイロードから除外されます。

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するには、次の構成を行います。

* **Pixel ID**：Reddit Pixel ID。
* **Send Page Visit**
    * デフォルトでは、サイトの各ページについてページ訪問イベントが自動的に記録されます。
    * ページ訪問イベントをReddit Pixelへ送信しない場合は、このオプションを`false`に構成します。
* **Send Default Purchase Event**：デフォルトでは、サイト上の購入イベントが追跡されます。購入イベントを無効にするには、このオプションを`false`に構成します。
* **Generate Event ID**：Redditの各トラッキングイベントに対してイベントIDを自動生成します。

### Conversions API


<blockquote>
この機能を使用するには、有効な[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Reddit Conversions APIをサポートするには、**Generate Event ID**を`true`に構成します。**Generate Event ID**を有効にすると、タグは追跡する各イベントに一意のイベントIDを生成します。タグは、Reddit Conversionsコネクタで使用できるようにイベントIDを属性としてEvent Streamingへ送信し、`event_id`パラメータでReddit Pixelに渡します。このイベントID属性をコネクタにマッピングし、Webベースのタグとサーバーサイド統合を同期します。

タグは、次の命名規則に従って生成されたイベント属性を使用し、イベントIDを送信します。

```nohl
reddit_pixel_event_id_{REDDIT_EVENT}_{TAG_UID}
```

たとえば、タグ#32からの購入イベントでは、次の属性と値が送信されます。

```json
{
  "reddit_pixel_event_id_Purchase_32": "028b2ade7478..."
}
```

同じタグからのページビューイベントでは、次の属性と値が送信されます。

```json
{
  "reddit_pixel_event_id_PageView_32": "084b1cda7461..."
}
```

#### 重複排除

イベントを適切に重複排除するには、Reddit PixelタグからのイベントIDを、Tealium Collectタグが送信するペイロードに含める必要があります。これを行うには、次の手順を実行します。

* **Tag Timing**ドロップダウンから、**Prioritized**を選択します。
* **Bundle Flag**トグルを`On`に構成します。
* [Load Order Manager画面](https://docs.tealium.com/load-order-manager/)を使用して、Reddit PixelタグがTealium Collectタグよりも先に発火するようにします。Tealium Collectタグは最後に発火させることをお勧めします。

これらのイベントID属性の使用方法については、[Reddit Conversionsコネクタ：Webイベントの重複排除](https://docs.tealium.com/reddit-conversions-connector/#deduplication-for-web-events)を参照してください。

## 検証

タグが期待どおりに動作していることを確認するには、ブラウザの開発者ツールと[Reddit Pixel Helper](https://business.reddithelp.com/s/article/Reddit-Pixel-Helper-Chrome-extension)ブラウザ拡張機能を使用します。

* イベントごとに、想定されるパラメータが表示されることを確認します。
* サポートされていないメタデータまたは無効なメタデータに関する警告が表示されていないことを確認します。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

以下のカテゴリを使用してパラメータをマッピングします。マッピングされたパラメータが特定のイベントについてRedditでサポートされていない場合、タグはそのパラメータをペイロードから除外します。イベントごとに送信するパラメータを制御するには、[イベント固有のパラメータ](#event-specific-parameters)を使用します。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数                    | データ型 | 説明                     |
|-------------------------|----------|--------------------------|
| `pixel_id`              | 文字列   | Pixel ID。                |
| `send_page_visit`       | ブール値 | ページ訪問を送信します。 |
| `send_purchase_event`   | ブール値 | 購入イベントを送信します。 |
| `generate_event_id`     | ブール値 | イベントIDを生成します。 |
| `event_id`              | 文字列   | イベントID。             |
| `conversion_id`         | 文字列   | コンバージョンID。       |
| `transaction_id`        | 文字列   | トランザクションID。     |

### Eコマース

| 変数            | データ型 | 説明                                 |
|-----------------|----------|--------------------------------------|
| `itemCount`     | 数値     | 商品数。                             |
| `value`         | 数値     | 値。                                 |
| `currency`      | 文字列   | 通貨（`_ccurrency`を上書きします）。 |
| `transactionId` | 文字列   | トランザクションID。                 |

### 商品データ

| 変数        | 型／値 | 説明                                      |
|:------------|:-------|:------------------------------------------|
| `id`        | 配列   | 商品ID（`_cprod`を上書きします）。       |
| `category`  | 配列   | 商品カテゴリ（`_ccat`を上書きします）。  |
| `name`      | 配列   | 商品名（`_cprodname`を上書きします）。   |
| `quantity`  | 配列   | 商品数量（`_cquan`を上書きします）。     |
| `itemPrice` | 配列   | 商品単価（`_cprice`を上書きします）。    |

### イベント

選択したイベントをトリガーするために必要な、マッピング対象変数の値を入力します。

| 変数             | 説明                   |
|:-----------------|:-----------------------|
| `PageVisit`      | ページ訪問。           |
| `ViewContent`    | コンテンツの表示。     |
| `Search`         | 検索。                  |
| `AddToCart`      | カートへの追加。       |
| `AddToWishlist`  | ウィッシュリストへの追加。 |
| `Purchase`       | 購入。                  |
| `Lead`           | リード。                |
| `SignUp`         | サインアップ。         |
| `Custom`         | カスタムイベント。     |
### イベント固有のパラメーター

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数            | 説明                      |
|:----------------|:--------------------------|
| `currency`      | 通貨。                    |
| `category`      | 商品カテゴリー。          |
| `name`          | 商品名。                  |
| `id`            | 商品 ID。                 |
| `quantity`      | 商品数量。                |
| `itemPrice`     | 商品単価。                |
| `content_type`  | コンテンツタイプ。        |
| `contents`      | コンテンツ。              |
| `predicted_ltv` | 予測顧客生涯価値。        |
| `search_string` | 検索文字列。              |
| `status`        | ステータス。              |
| `itemCount`     | アイテム数。              |
| `value`         | 値。                      |

### 高度なマッチング

| 変数          | データ型 | 説明                  |
|:--------------|:---------|:----------------------|
| `email`       | 文字列   | メールアドレス。      |
| `phoneNumber` | 文字列   | 電話番号。            |
| `idfa`        | 文字列   | IDFA。                 |
| `aaid`        | 文字列   | AAID。                 |
| `externalId`  | 文字列   | 外部 ID。              |

### LDU

Reddit Pixel がデータ処理モードで初期化されると、ページから送信されるすべてのコンバージョンイベントに、以下のパラメーターが自動的に含まれます。

| 変数    | データ型 | 説明 |
|:--------|:---------|:-----|
| `dpm`   | 文字列   | データ処理モード。デフォルト値は `LDU` です。 |
| `dpcc`  | 文字列   | ISO 3166-1 alpha-2 国コード形式のデータ処理国コード。 |
| `dprc`  | 文字列   | ISO 3166-2 地域コード形式のデータ処理地域コード。国プレフィックスの有無は問いません。 |