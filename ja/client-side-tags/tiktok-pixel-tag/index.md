---
title: TikTok Pixel タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントで TikTok Pixel タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/tiktok-pixel-tag/
---
## タグのヒント

*   マッピングを使用して、タグ構成をオーバーライドし、動的に構成します。
*   デフォルトでは、タグテンプレートはマップされた製品パラメータがイベントごとに単一の製品か複数の製品かを検出します。単一の製品が検出された場合、個々のTikTok製品変数（`content_id`、`content_category`、`content_name`）が使用されます。複数の製品が検出された場合、`contents` 配列が自動的に生成され使用されます。
*   デフォルトでは、ユーザーデータ（ハッシュ化された、または非ハッシュ化されたメールアドレスまたは電話番号）が入力された各イベントに対して `Identify` メソッドが自動的に送信されます。タグ構成でこれを無効にします。ベストプラクティスとして、TikTokは顧客情報をサーバーに入力する前にSHA256で自動的にハッシュ化します。
*   TikTokが非ハッシュ化されたメールを収集するには、値に `@` 文字が含まれている必要があり、ドメイン指定で終わる必要があります。
*   TikTokが非ハッシュ化された電話番号を収集するには、値が E.164 形式に従う必要があります: `&#43;{国コード}{電話番号}`。例えば、`&#43;14135552671`（米国）、`&#43;442071838750`（英国）、`&#43;551155256325`（ブラジル）。
*   ハッシュ化されたメールアドレスと電話番号の値を暗号化して入力するために、Crypto Extensionを使用します。
*   `value` パラメータは、製品の価格と数量に基づいて自動的に計算され構成されます。
*   デフォルトでは、TikTokピクセルベースコードはすべてのページで `Pageview` イベントを追跡します。タグ構成またはデータマッピングで `auto_page_tracking` を使用してこれを無効にします。
*   デフォルトでは、注文IDが入力されたときに `CompletePayment` イベントが発生します。タグ構成またはデータマッピングで `auto_purchase_tracking` を使用してこれを無効にします。

  カスタムまたは非標準のパラメータはTikTokによって処理されません。広告主はTikTokアカウント担当者にカスタムレポートを依頼して、カスタムパラメータのメトリクスを計算することができます。

## タグ構成

タグマーケットプレイスにアクセスして新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際に、以下の構成を構成します：

* **Pixel ID**: あなたのTikTok Pixel ID。
* **Content Type**: `content_type` を構成して、製品カタログの形式に基づいて製品を追跡する方法を決定します。個々の製品（通常はSKUとしてフォーマットされます）に関連するイベントを追跡するために `Product` を選択するか、製品グループ（製品IDのプレフィックスが多い）に関連するイベントを追跡するために `Product Group` を選択します。詳細については、[TikTok: パラメータについて](https://ads.tiktok.com/help/article/about-parameters?lang=en)を参照してください。
* **Generate Event ID**: 有効にする場合、[TikTok Events connector]()と連携してイベントIDパラメータをマッピングし、ウェブとサーバーベースの統合を同期します。この機能にはアクティブなTealium Collectタグが必要です。
* **Automatic Pageview Tracking**: すべてのページで `Pageview` イベントを自動的に追跡します。この構成を `auto_page_tracking` をマッピングしてオーバーライドします。
* **Automatic Purchase Tracking**: 注文IDが検出されたときに `CompletePayment` イベントを自動的に追跡します。この構成を `auto_purchase_tracking` をマッピングしてオーバーライドします。
* **Automatic Identity Tracking**: 顧客情報（メール、電話番号、その他の識別子）をウェブサイトでの人々の行動と照合するのに役立つTikTok Advanced Matching機能を有効にします。有効にすると、タグはユーザーデータ（メールまたは電話番号）が検出されるたびに `ttq.identify()` を呼び出します。詳細については、[TiKTok: ウェブ用高度なマッチングについて](https://ads.tiktok.com/help/article/advanced-matching-web)を参照してください。
* **Limited Data Use**: 特定の米国州のプライバシー法に基づいて個人データの販売および共有のオプトアウト権を行使する広告主を支援する機能です。詳細については、[TikTok: Limited Data Use](https://business-api.tiktok.com/portal/docs?id=1770092377990145)を参照してください。

## ロードルール

すべてのページでタグをロードするか、タグのロード条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### タグ構成

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `pixel_code`  | 文字列 | Pixel ID。 |
|  `content_type`  | 文字列 | コンテンツタイプ。 |
|  `auto_page_tracking`  | ブール値 | 自動ページビュー追跡。 |
|  `auto_purchase_tracking`  | ブール値 | 自動購入追跡。 |
|  `auto_identity_tracking`  | ブール値 | 自動アイデンティティ追跡。 |
|  `ldu`  | ブール値 | 限定データ使用。 |

### ユーザーパラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `email`  | 文字列 | ユーザーのメール。| 
|  `phone_number`  | 文字列 | ユーザーの電話番号。| 
|  `sha256_email`  | 文字列 | ユーザーのハッシュ化されたメール。| 
| `sha256_phone_number`  | 文字列 | ユーザーのハッシュ化された電話番号。 | 
| `external_id`| 文字列 | 広告主のプラットフォーム上のユーザーを表す識別子（顧客ID、ロイヤルティカード番号、注文IDなど）。プレーンテキストで提供された場合、TikTokライブラリは摂取前にIDをハッシュ化します。 | 
| `sha256_external_id`| 文字列 | 広告主のプラットフォーム上のユーザーを表すSHA256ハッシュ化された識別子（顧客ID、ロイヤルティカード番号、注文IDなど）。ハッシュ化する前に先頭と末尾のスペースをトリミングします。 | 

### 標準トラッキングパラメータ

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `currency`   | 文字列 | 通貨（`_ccurrency`をオーバーライド）。 |
|  `value`   | 数値 | 価値（`_ctotal`をオーバーライド）。 |
|  `query`  | 文字列 | クエリ。 |
|  `description`  | 文字列 | 説明。 |
|  `status`  | 文字列 | 状態。 |
|  `contents`  | オブジェクトの配列 | コンテンツ。 |
|  `content_id`   | 文字列の配列 | コンテンツID（`_cprod`をオーバーライド）。 |
|  `content_name`  | 文字列の配列 | コンテンツ名（`_cprodname`をオーバーライド）。 |
|  `content_category`   | 文字列の配列 | コンテンツカテゴリ（`_ccat`をオーバーライド）。 |
|  `quantity`   | 数値の配列 | 数量（`_cquan`をオーバーライド）。 | 
|  `price`   | 数値の配列 | 価格（`_cprice`をオーバーライド）。 |

### イベント

イベントマッピングの作成についての詳細は、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `AddPaymentInfo` | 決済情報を追加 |
| `AddToCart` | カートに追加 |
| `AddToWishlist` | ほしい物リストに追加 |
| `ClickButton` | ボタンをクリック |
| `CompletePayment` | 決済完了 |
| `CompleteRegistration` | 登録完了 |
| `Contact` | 連絡 |
| `Download` | ダウンロード |
| `InitiateCheckout` | チェックアウト開始 |
| `PlaceAnOrder` | 注文 |
| `Search` | 検索 |
| `SubmitForm` | フォームを送信 |
| `Subscribe` | 登録 |
| `ViewContent` | コンテンツを表示 |
| `Custom` | カスタム |



### 旅行 - ホテルのパラメータ

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `hotel.content_id` | `String or Array of Strings` | イベントに関連する製品ID、例えばSKU |
| `hotel.city` | `String` | ホテルの都市 |
| `hotel.region` | `String` | ホテルの地域 |
| `hotel.country` | `String` | ホテルの国 |
| `hotel.checkin_date` | `String` | ホテルのチェックイン日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。 |
| `hotel.checkout_date` | `String` | ホテルのチェックアウト日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。 |
| `hotel.num_adults` | `Number` | 大人の数 |
| `hotel.num_children` | `Number` | 子供の数 |
| `hotel.suggested_hotels` | `String or Array of Strings` | このユーザーに推奨されるホテル |

### 旅行 - フライトのパラメータ

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `flight.content_id` | `String or Array of Strings` | イベントに関連する製品ID、例えばSKU |
| `flight.destination_city` | `String` | 目的地の都市名 |
| `flight.departing_departure_date` | `String` | 出発フライトの離陸日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。 |
| `flight.departing_arrival_date` | `String` | 出発フライトの着陸日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。|
| `flight.returning_departure_date` | `String` | 帰りのフライトの離陸日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。|
| `flight.returning_arrival_date` | `String` | 帰りのフライトの着陸日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。|
| `flight.origin_airport` | `String` | 出発空港コード、例えば `JFK` |
| `flight.destination_airport` | `String` | 目的地空港コード、例えば `CDG` |
| `flight.num_adults` | `Number` | 大人の数 |
| `flight.num_children` | `Number` | 子供の数 |
| `flight.num_infants` | `Number` | 幼児の数 |
| `flight.travel_class` | `String` | フライトチケットのクラス。受け入れられる値: `eco`, `prem`, `bus`, `first`。 |
| `flight.user_score` | `Number` | この潜在顧客の広告主に対する相対的な価値を表す |
| `flight.preferred_num_stops` | `Number` | 希望の停留回数 |

### 旅行 - 目的地のパラメータ

| 変数 | 型/値 | 説明 |
|:---------|:-----|:------------|
| `destination.content_id` | `String or Array of Strings` | イベントに関連する製品ID、例えばSKU |
| `destination.city` | `String` | 目的地の都市 |
| `destination.region` | `String` | 目的地の地域 |
| `destination.country` | `String` | 目的地の国 |
| `destination.travel_start` | `String` | ユーザーの旅行開始日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。 |
| `destination.travel_end` | `String` | ユーザーの旅行終了日。受け入れられる日付形式: `YYYYMMDD`, `YYYY-MM DD`, `YYYY-MM-DDThh:mmTZD`, `YYYY-MM-DDThh:mm:ssTZD`。例: `20250623`, `2025-06-23`,`2025-06-23T15:30GMT`, `2025-06-23T15:30:00GMT`。 |
| `destination.num_adults` | `Number` | 大人の数 |
| `destination.num_children` | `Number` | 子供の数 |
| `destination.num_infants` | `Number` | 幼児の数 |
| `destination.suggested_destinations` | `String or Array of Strings` | このユーザーに提案される目的地のIDリスト |
