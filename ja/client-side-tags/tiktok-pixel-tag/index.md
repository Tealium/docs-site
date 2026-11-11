---
title: TikTok Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでTikTok Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tiktok-pixel-tag/
---
## タグに関するヒント

*   マッピングを使用して、タグ構成を上書きしたり動的に構成したりできます。
*   デフォルトでは、タグテンプレートは、マッピングされた商品パラメータにイベントごとに単一の商品が含まれているか、複数の商品が含まれているかを検出します。単一の商品が検出された場合は、個別のTikTok商品変数（`content_id`、`content_category`、`content_name`）が使用されます。複数の商品が検出された場合は、`contents`配列が自動的に構成され、使用されます。
*   デフォルトでは、ユーザーデータ（ハッシュ化済みまたは未ハッシュ化のメールアドレスまたは電話番号）が構成されている各イベントに対して、`Identify`メソッドが自動的に送信されます。この動作はタグ構成で無効にできます。ベストプラクティスとして、TikTokは照合のために顧客の未加工情報がTikTokのサーバーに送信される前に、SHA256で自動的にハッシュ化します。
*   TikTokが未ハッシュ化のメールアドレスを収集するには、値に`@`文字が含まれ、末尾がドメイン名である必要があります。
*   TikTokが未ハッシュ化の電話番号を収集するには、値がE.164形式（`+{country code}{phone number}`）に従っている必要があります。例：`+14135552671`（米国）、`+442071838750`（英国）、`+551155256325`（ブラジル）。
*   Crypto Extensionを使用して、ハッシュ化されたメールアドレスと電話番号の値を暗号化して構成します。
*   `value`パラメータは、商品の価格と数量に基づいて自動的に計算および構成されます。
*   デフォルトでは、TikTok Pixelのベースコードはすべてのページで`Pageview`イベントをトラッキングします。この動作は、タグ構成または`auto_page_tracking`のデータマッピングで無効にできます。
*   デフォルトでは、注文IDが構成されると`CompletePayment`イベントが発生します。この動作は、タグ構成または`auto_purchase_tracking`のデータマッピングで無効にできます。
*   Pageviewイベントを手動で管理するシングルページアプリケーションでは、**履歴オブザーバー**を`false`に構成し、**自動Pageviewトラッキング**を無効にします。その後、アプリケーションのルートが変更されるたびに、明示的なTealium Pageviewイベントを送信します。これにより、ブラウザー履歴の変更時にTikTokのライブラリから重複したPageviewイベントが発生するのを防ぎます。

  
<blockquote>
カスタムパラメータまたは標準外のパラメータは、TikTokでは処理されません。広告主はTikTokアカウントの担当者にカスタムレポートを依頼し、カスタムパラメータの指標を計算できます。
</blockquote>


## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Pixel ID**：TikTok Pixel ID。
* **コンテンツタイプ**：商品カタログの形式に基づいて商品をトラッキングする方法を決定するため、`content_type`を構成します。個々の商品（一般的にはSKU形式）に関連付けられたイベントをトラッキングするには`Product`を選択し、商品グループ（多くの場合、商品IDのプレフィックス）に関連付けられたイベントをトラッキングするには`Product Group`を選択します。詳細については、[TikTok：パラメータについて](https://ads.tiktok.com/help/article/about-parameters?lang=en)を参照してください。
* **イベントIDを生成**：有効にした場合は、[TikTok Eventsコネクタ](https://docs.tealium.com/tiktok-events-connector/)と併用し、コネクタのイベントIDパラメータをマッピングして、Webベースとサーバーベースの統合を同期します。この機能を使用するには、有効なTealium Collectタグが必要です。
* **自動Pageviewトラッキング**：すべてのページで`Pageview`イベントを自動的にトラッキングします。`auto_page_tracking`をマッピングすることで、この構成を上書きできます。
* **自動購入トラッキング**：注文IDが検出されたときに、`CompletePayment`イベントを自動的にトラッキングします。`auto_purchase_tracking`をマッピングすることで、この構成を上書きできます。
* **自動IDトラッキング**：メールアドレス、電話番号、その他の識別子などの顧客情報と、ユーザーがWebサイトで行ったアクションとの照合に役立つTikTok Advanced Matching機能を有効にします。有効にすると、ユーザーデータ（メールアドレスまたは電話番号）が検出されたすべてのイベントで、タグが`ttq.identify()`を呼び出します。詳細については、[TikTok：Web向けAdvanced Matchingについて](https://ads.tiktok.com/help/article/advanced-matching-web)を参照してください。
* **データ使用の制限**：米国の一部の州のプライバシー法に基づき、個人データの販売および共有をオプトアウトする権利への広告主の準拠を支援する機能です。詳細については、[TikTok：データ使用の制限](https://business-api.tiktok.com/portal/docs?id=1770092377990145)を参照してください。
* **履歴オブザーバー**：SPAのブラウザー履歴が変更されたときに、TikTokがPageviewイベントを自動的に報告するかどうかを制御します。TikTokによるSPA履歴の自動トラッキングを無効にするには、`false`に構成します。構成しない場合、TikTokのデフォルト動作が維持されます。詳細については、[TikTok：シングルページアプリケーションの操作](https://business-api.tiktok.com/portal/docs?id=1801524003169281)を参照してください。

## ロードルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグの対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは次のとおりです。

### タグ構成

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `pixel_code`  | 文字列 | Pixel ID。 |
|  `content_type`  | 文字列 | コンテンツタイプ。 |
|  `auto_page_tracking`  | ブール値 | 自動Pageviewトラッキング。 |
|  `auto_purchase_tracking`  | ブール値 | 自動購入トラッキング。 |
|  `auto_identity_tracking`  | ブール値 | 自動IDトラッキング。 |
|  `ldu`  | ブール値 | データ使用の制限。 |
|  `historyObserver`  | ブール値 | SPAのブラウザー履歴が変更されたときに、TikTokがPageviewイベントを自動的に報告するかどうかを制御します。TikTokによるSPA履歴の自動トラッキングを無効にするには、`false`に構成します。マッピングされていない場合、TikTokのデフォルト動作が維持されます。 |

### ユーザーパラメータ

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `email`  | 文字列 | ユーザーのメールアドレス。| 
|  `phone_number`  | 文字列 | ユーザーの電話番号。| 
|  `sha256_email`  | 文字列 | ユーザーのハッシュ化されたメールアドレス。| 
| `sha256_phone_number`  | 文字列 | ユーザーのハッシュ化された電話番号。 | 
| `external_id`| 文字列 | 顧客ID、ロイヤルティカード番号、注文IDなど、広告主のプラットフォーム上のユーザーを表す識別子。プレーンテキストで指定した場合、TikTokライブラリは取り込み前にIDをハッシュ化します。 | 
| `sha256_external_id`| 文字列 | 顧客ID、ロイヤルティカード番号、注文IDなど、広告主のプラットフォーム上のユーザーを表すSHA256でハッシュ化された識別子。ハッシュ化する前に、先頭または末尾のスペースを削除してください。 | 

### 標準トラッキングパラメータ

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
|  `currency`   | 文字列 | 通貨（`_ccurrency`を上書き）。 |
|  `value`   | 数値 | 値（`_ctotal`を上書き）。 |
|  `query`  | 文字列 | クエリ。 |
|  `description`  | 文字列 | 説明。 |
|  `status`  | 文字列 | ステータス。 |
|  `contents`  | オブジェクトの配列 | コンテンツ。 |
|  `content_id`   | 文字列の配列 | コンテンツID（`_cprod`を上書き）。 |
|  `content_name`  | 文字列の配列 | コンテンツ名（`_cprodname`を上書き）。 |
|  `content_category`   | 文字列の配列 | コンテンツカテゴリ（`_ccat`を上書き）。 |
|  `quantity`   | 数値の配列 | 数量（`_cquan`を上書き）。 | 
|  `price`   | 数値の配列 | 価格（`_cprice`を上書き）。 |

### イベント

イベントのマッピングについて詳しくは、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `AddPaymentInfo` | AddPaymentInfo |
| `AddToCart` | AddToCart |
| `AddToWishlist` | AddToWishlist |
| `ClickButton` | ClickButton |
| `CompletePayment` | CompletePayment |
| `CompleteRegistration` | CompleteRegistration |
| `Contact` | Contact |
| `Download` | Download |
| `InitiateCheckout` | InitiateCheckout |
| `PlaceAnOrder` | PlaceAnOrder |
| `Search` | Search |
| `SubmitForm` | SubmitForm |
| `Subscribe` | Subscribe |
| `ViewContent` | ViewContent |
| `Custom` | Custom |
### 旅行 - ホテルのパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `hotel.content_id` | `String or Array of Strings` | SKU など、イベントに関連付けられた商品 ID |
| `hotel.city` | `String` | ホテルが所在する都市 |
| `hotel.region` | `String` | ホテルが所在する地域 |
| `hotel.country` | `String` | ホテルが所在する国 |
| `hotel.checkin_date` | `String` | ホテルのチェックイン日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。 |
| `hotel.checkout_date` | `String` | ホテルのチェックアウト日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。 |
| `hotel.num_adults` | `Number` | 大人の人数 |
| `hotel.num_children` | `Number` | 子供の人数 |
| `hotel.suggested_hotels` | `String or Array of Strings` | このユーザーへのおすすめホテル |


### 旅行 - フライトのパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `flight.content_id` | `String or Array of Strings` | SKU など、イベントに関連付けられた商品 ID。 |
| `flight.destination_city` | `String` | 目的地の都市名 |
| `flight.departing_departure_date` | `String` | 往路便の離陸日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。 |
| `flight.departing_arrival_date` | `String` | 往路便の着陸日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。|
| `flight.returning_departure_date` | `String` | 復路便の離陸日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。|
| `flight.returning_arrival_date` | `String` | 復路便の着陸日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。|
| `flight.origin_airport` | `String` | 出発空港のコード（例：`JFK`） |
| `flight.destination_airport` | `String` | 到着空港のコード（例：`CDG`） |
| `flight.num_adults` | `Number` | 人数 |
| `flight.num_children` | `Number` | 子供の人数 |
| `flight.num_infants` | `Number` | 乳幼児の人数 |
| `flight.travel_class` | `String` | 航空券のクラス。使用できる値：`eco`、`prem`、`bus`、`first`。 |
| `flight.user_score` | `Number` | この見込み顧客が広告主にとって持つ相対的な価値 |
| `flight.preferred_num_stops` | `Number` | 希望する経由地の数 |


### 旅行 - 目的地のパラメーター

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `destination.content_id` | `String or Array of Strings` | SKU など、イベントに関連付けられた商品 ID |
| `destination.city` | `String` | 目的地の都市 |
| `destination.region` | `String` | 目的地の地域 |
| `destination.country` | `String` | 目的地の国 |
| `destination.travel_start` | `String` | ユーザーの旅行開始日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。 |
| `destination.travel_end` | `String` | ユーザーの旅行終了日。使用できる日付形式：`YYYYMMDD`、`YYYY-MM DD`、`YYYY-MM-DDThh:mmTZD`、`YYYY-MM-DDThh:mm:ssTZD`。例：`20250623`、`2025-06-23`、`2025-06-23T15:30GMT`、`2025-06-23T15:30:00GMT`。 |
| `destination.num_adults` | `Number` | 人数 |
| `destination.num_children` | `Number` | 子供の人数 |
| `destination.num_infants` | `Number` | 乳幼児の人数 |
| `destination.suggested_destinations` | `String or Array of Strings` | このユーザーへのおすすめ目的地を表す ID のリスト |