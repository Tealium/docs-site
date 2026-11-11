---
title: ChatGPT Ads Measurement Pixelタグ
description: この記事では、タグ管理アカウントでChatGPT Ads Measurement Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/chatgpt-ads-measurement-pixel-tag/
---
ChatGPT Ads Measurement Pixelを使用すると、Webサイト上のコンバージョンや顧客のアクションを測定し、ChatGPT Adsキャンペーンを最適化できます。

## タグに関するヒント

* **Events**タブを使用して、データレイヤー変数をChatGPT Adsの標準イベントタイプのいずれかに関連付けます。タグは、一致したトリガーごとに1回の測定を送信します。
* **Configuration**タブを使用すると、実行ごとに**Pixel ID**または**Custom SDK URL**を上書きできます（マルチブランドプロファイルなど）。イベントレベルのオプションと同意には**General**タブを、注文合計、通貨、商品ごとの配列には**E-Commerce**タブを使用します。単一イベントについてこれらを上書きするには、**Event-specific Parameters**タブを使用します。
* グローバル値は、イベントごとに自動的にフィルタリングされます。たとえば、`plan_id`は`subscription_created`、`trial_started`、`custom`イベントにのみエンリッチメントされます。
* デフォルトでは、ページビューと購入が自動的に送信されます。無効にするには、**Auto Page View**オプションと**Auto Order Created**オプションを使用します。
* 次のE-Commerce拡張パラメータをサポートします。
    * 小計（`_csubtotal`）
    * 通貨（`_ccurrency`）
    * 注文ID（`_corder`）
    * 商品IDのリスト（`_cprod`）
    * 商品名のリスト（`_cprodname`）
    * カテゴリのリスト（`_ccat`）
    * 数量のリスト（`_cquan`）
    * 価格のリスト（`_cprice`）
* **Amount**と**Product Amount**は主要通貨単位（例：129.99）でマッピングされます。タグは、ChatGPT Ads Measurement Pixel APIに合わせて整数の補助通貨単位に変換します。
* **Product Type**がマッピングされていない場合、すべての呼び出しがベンダーの検証を通過するように、コンテンツタイプのデフォルト値として`product`が使用されます。
* カスタムChatGPT Adsイベントを送信するには、**Events**タブまたは**Event-specific Parameters**タブで**Custom**を選択し、表示されるフィールドにベンダーのイベント名を入力します。ここでマッピングされたイベント名がChatGPT Adsの標準イベントリストにない場合、その名前を持つ`custom`イベントとして自動的にルーティングされます。
* **Pixel ID**は、OpenAIのアカウントチームから取得してください。ChatGPT Ads Managerを使用したセルフサービスでのプロビジョニングはサポートされていません。
* `utag.gdpr.getConsentState()`を通じてTealiumの同意状態を尊重し、同意が拒否された場合は送信をスキップします。許可または取り消しをMeasurement Pixel SDKに直接転送するには、**Consent**の送信先をマッピングします。
* 高度なコンバージョンマッチング用にハッシュ化された識別情報を送信するには、**User data**マッピングを使用します。電話番号、名、姓は正規化され、送信前にSHA-256でハッシュ化されます。地域と郵便番号は未加工の文字列として送信されます。正規化をスキップして値をそのまま送信するには、事前にハッシュ化された値（小文字の64文字の16進数）を指定します。
* OpenAI Measurement Pixelでは、ブラウザー内でサポート対象の識別情報を検出してハッシュ化する、自動高度マッチングがサポートされています。アカウントで自動高度マッチングが有効になっている場合は、ユーザーデータの重複送信を防ぐため、同じフィールドを手動でマッピングしないでください。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を行います。

* **Pixel ID**：ChatGPT AdsのPixel ID。OpenAIのアカウントチームからこの値を取得してください。
* **Debug Mode**：ブラウザーコンソールでMeasurement Pixel SDKのデバッグログを有効にします。
* **Custom SDK URL**：（任意）ベースURLを上書きします。
* **Auto Page View**：Tealiumの各ビューイベントで`page_viewed`を自動的にキューに追加します（デフォルトは`true`）。明示的な**Events**タブのトリガーによって`page_viewed`がすでにキューに追加されている場合はスキップします。
* **Auto Order Created**：**E-Commerce**拡張機能によって`_corder`に値が構成され、`order_created`がまだキューに追加されていない場合に、`order_created`を自動的にキューに追加します（デフォルトは`true`）。
* **Generate Event ID**：OpenAIの各トラッキングイベントに対して一意のイベントIDを自動生成します。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用できるカテゴリは次のとおりです。

### 構成

| 変数 | タイプ／値 | 説明 |
|:---------|:-----|:------------|
| `pixel_id` | `String` | Pixel ID |
| `custom_sdk_url` | `String` | カスタムSDK URL |


### 全般

| 変数 | タイプ／値 | 説明 |
|:---------|:-----|:------------|
| `event_id` | `String` | イベントID |
| `plan_id` | `String` | プランID |
| `consent` | `String` | 同意 |


### ユーザーデータ

OpenAI Measurement Pixelの初期化時に、ユーザーデータフィールドが`init.user`オブジェクトに配置されます。識別情報フィールドは正規化され、SHA-256でハッシュ化されます。地理情報フィールドは未加工の文字列として送信されます。

詳細については、[OpenAI Measurement Pixel：ユーザーデータの送信](https://developers.openai.com/ads/measurement-pixel#send-user-data)を参照してください。

| 変数 | タイプ／値 | 説明 |
|:---------|:-----|:------------|
| `phone_number_sha256` | `String` | 電話番号。正規化（国番号は保持し、空白、句読点、先頭の`+`、先頭のゼロを削除）した後、SHA-256でハッシュ化されます。事前にハッシュ化された値（小文字の64文字の16進数）は、変更されずにそのまま渡されます。 |
| `first_name_sha256` | `String` | 名。小文字に変換し、空白とASCII句読点を削除（非ASCII文字は保持）した後、SHA-256でハッシュ化されます。事前にハッシュ化された値は、変更されずにそのまま渡されます。 |
| `last_name_sha256` | `String` | 姓。小文字に変換し、空白とASCII句読点を削除（非ASCII文字は保持）した後、SHA-256でハッシュ化されます。事前にハッシュ化された値は、変更されずにそのまま渡されます。 |
| `region` | `String` | 州、省、または地域。未加工の文字列として送信されます。最大128文字です。 |
| `postal_code` | `String` | 郵便番号またはZIPコード。未加工の文字列として送信されます。最大32文字です。 |


### E-Commerce

| 変数 | タイプ／値 | 説明 |
|:---------|:-----|:------------|
| `amount` | `Integer` | 金額（`_csubtotal`を上書き） |
| `currency` | `String` | 通貨（`_ccurrency`を上書き） |
| `product_id` | `Array` | 商品ID（`_cprod`を上書き） |
| `product_name` | `Array` | 商品名（`_cprodname`を上書き） |
| `product_type` | `Array` | 商品タイプ（`_ccat`を上書き） |
| `product_quantity` | `Array` | 商品数量（`_cquan`を上書き） |
| `product_amount` | `Array` | 商品金額（`_cprice`を上書き） |
| `product_currency` | `Array` | 商品通貨（`_ccurrency`を上書き） |


### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `event_id` | イベントID |
| `amount` | 金額（`_csubtotal`を上書き） |
| `currency` | 通貨（`_ccurrency`を上書き） |
| `plan_id` | プランID |
| `id` | 商品ID（`_cprod`を上書き） |
| `name` | 商品名（`_cprodname`を上書き） |
| `content_type` | 商品タイプ（`_ccat`を上書き） |
| `quantity` | 商品数量（`_cquan`を上書き） |
| `amount` | 商品金額（`_cprice`を上書き） |
| `currency` | 商品通貨（`_ccurrency`を上書き） |