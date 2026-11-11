---
title: Roku JavaScript Pixelタグ構成ガイド
description: この記事では、Roku JavaScript Pixelタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/roku-javascript-pixel-tag/
---
## タグに関するヒント

* マッピングを使用して標準パラメータを上書きします。
* Eコマース拡張機能のパラメータをサポートしています。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、次の構成を行います。

* **広告アカウントID**：Roku広告アカウントID。
* **イベントIDを生成**：Rokuの各トラッキングイベントに対してイベントIDを自動的に生成します。Roku Events APIコネクタを実装する際の重複排除に使用されます。デフォルト値は`true`です。詳細については、[Roku Events APIコネクタ](https://docs.tealium.com/roku-events-api-connector/)を参照してください。
* **ページビューの自動トラッキング**：ページビューを自動的にトラッキングします。デフォルト値は`true`です。
* **購入の自動トラッキング**：`order_id`または`_corder`が存在する場合、購入イベントを自動的にトリガーします。デフォルト値は`true`です。

### Roku Events API


<blockquote>
この機能を使用するには、有効な[Tealium Collectタグ](https://docs.tealium.com/tealium-collect-tag/)が必要です。
</blockquote>


Roku Events APIをサポートするには、**イベントIDを生成**を`true`に構成します。**イベントIDを生成**を有効にすると、このタグはトラッキングされるイベントごとに一意のイベントIDを生成し、Roku Events APIコネクタで使用できるように属性としてEvent Streamingに送信します。また、そのIDを`event_id`パラメータでRoku JavaScript Pixelに渡します。このイベントID属性をコネクタでマッピングすることで、Webベースのタグとサーバーサイド統合を同期できます。

タグは、次の命名規則に従って生成されたイベント属性を使用してイベントIDを送信します。

```nohl
roku_event_id_{EVENT_NAME}_{TAG_UID}
```

たとえば、タグ#32からの購入イベントでは、次の属性と値が送信されます。

```json
{
  "roku_event_id_purchase_32": "028b2ade7478..."
}
```

同じタグからのページビューイベントでは、次の属性と値が送信されます。

```json
{
  "roku_event_id_page_view_32": "084b1cda7461..."
}
```

#### 重複排除

イベントが適切に重複排除されるようにするには、Roku Events APIコネクタのPixelタグからのイベントIDを、Tealium Collectタグが送信するペイロードに含める必要があります。これを行うには、次の手順を実行します。

* **タグのタイミング**ドロップダウンから、**優先**を選択します。
* **バンドルフラグ**トグルを`On`に構成します。
* **ロード順序マネージャー**を使用して、Roku JavaScript PixelタグをTealium Collectタグより先に実行します。Tealium Collectタグは最後に実行することをお勧めします。詳細については、[ロード順序マネージャー](https://docs.tealium.com/load-order-manager/)を参照してください。

これらのイベントID属性の使用方法については、[Roku：Events APIコネクタ](https://docs.tealium.com/roku-events-api-connector/)および[Roku：Conversions API](https://help.ads.roku.com/en/articles/8880744-conversions-api)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグの構成

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `account_id` | 文字列 | アカウントID。 |
| `generate_event_id` | ブール値 | イベントIDを生成します。 |
| `auto_page_view` | ブール値 | ページビューを自動的にトラッキングします。 |
| `auto_purchase_event` | ブール値 | 購入イベントを自動的にトラッキングします。 |

### ユーザー

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `user_data.is_hashed` | ブール値 | ハッシュ化されているかどうか。 |
| `user_data.em` | 文字列 | メールアドレス。 |
| `user_data.ph` | 文字列 | 電話番号。 |
| `user_data.ge` | 文字列 | 性別。 |
| `user_data.db` | 文字列 | 生年月日。 |
| `user_data.ln` | 文字列 | 姓。 |
| `user_data.fn` | 文字列 | 名。 |
| `user_data.ct` | 文字列 | 市区町村。 |
| `user_data.st` | 文字列 | 州。 |
| `user_data.zp` | 文字列 | 郵便番号。 |
| `user_data.country` | 文字列 | 国。 |
| `user_data.external_id` | 文字列 | 外部ID。 |
| `user_data.subscription_id` | 文字列 | サブスクリプションID。 |
| `user_data.ga_session_id` | 文字列 | Google AnalyticsセッションID。 |
| `user_data.ga_client_id` | 文字列 | Google AnalyticsクライアントID。 |
| `user_data.ga_gclid` | 文字列 | Google AnalyticsクリックID。 |
| `user_data.ga_measurement_ids` | 配列 | Google Analytics測定ID。 |
| `user_data.us_privacy` | 文字列 | 米国プライバシー文字列。 |

### Eコマース

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | 文字列 | 注文ID（`_corder`を上書き）。 |
| `order_subtotal` | 文字列 | 小計（`_csubtotal`を上書き）。 |
| `order_currency` | 文字列 | 通貨（`_ccurrency`を上書き）。 |
| `delivery_category` | 文字列 | 配送カテゴリ。 |
| `product_delivery_category` | 配列 | 商品の配送カテゴリのリスト。 |
| `product_id` | 配列 | 商品IDのリスト（`_cprod`を上書き）。 |
| `product_quantity` | 配列 | 商品数量のリスト（`_cquan`を上書き）。 |
| `product_unit_price` | 配列 | 商品価格のリスト（`_cprice`を上書き）。 |

### 標準トラッキングパラメータ

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `event_id` | 文字列 | イベントID。|
| `content_category` | 文字列または配列 | コンテンツカテゴリ。 |
| `content_name` | 文字列または配列 | コンテンツ名。 |
| `content_ids` | 配列 | コンテンツID。 |
| `content_type` | 文字列 | コンテンツタイプ。 |
| `predicted_ltv` | 文字列 | 予測顧客生涯価値。 |
| `search_string` | 文字列 | 検索文字列。 |
| `num_items` | 数値 | アイテム数。 |
| `status` | 文字列 | ステータス。 |
| `event_source` | 文字列 | イベントソース。 |
| `event_source_URL` | 文字列 | イベントソースURL。 |
| `referrer_URL` | 文字列 | 参照元URL。 |
| `opt_out` | 文字列 | LDUオプトアウト。 |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `event_id` | イベントID。 |
| `content_category` | コンテンツカテゴリ。 |
| `content_name` | コンテンツ名。 |
| `content_ids` | コンテンツID（`_cprod`を上書き）。 |
| `content_type` | コンテンツタイプ。 |
| `predicted_ltv` | 予測顧客生涯価値。 |
| `search_string` | 検索文字列。 |
| `num_items` | アイテム数。 |
| `status` | ステータス。 |
| `event_source` | イベントソース。 |
| `event_source_URL` | イベントソースURL。 |
| `referrer_URL` | 参照元URL。 |
| `opt_out` | LDUオプトアウト。 |
| `order_id` | 注文ID。 |
| `order_subtotal` | 小計。 |
| `order_currency` | 通貨。 |
| `delivery_category` | 配送カテゴリ。 |
| `product_delivery_category` | 商品の配送カテゴリのリスト。 |
| `product_id` | 商品IDのリスト。 |
| `product_quantity` | 商品数量のリスト。 |
| `product_unit_price` | 商品価格のリスト。 |