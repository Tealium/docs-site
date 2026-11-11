---
title: Facebook App Analyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでFacebook App Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/facebook-app-analytics-tag/
---
## タグに関するヒント

* Facebook Developerドキュメント
  * [API v2.12](https://developers.facebook.com/docs/marketing-api/app-event-api/v2.12)
  * [アプリケーションアクティビティ](https://developers.facebook.com/docs/graph-api/reference/application/activities/)

* タグ構成
  * これらはダッシュボードで確認できます
  * APIバージョン
  * APP ID
  * APPトークン（APPシークレット）

## タグ構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を構成します。

* **アプリケーションID**：整数値（例：`123456`）
* **アクセストークン（Appシークレット）**：整数値（例：`123456`）
* **イベント名**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

|説明| パラメータ|
|---| ---|
|App ID| `app_id`|
|アクセストークン| `access_token`|
|イベント名| `event_name`|
|広告主ID| `advertiser_id`|
|アトリビューション| `attribution`|
|広告主トラッキングが有効| `advertiser_tracking_enabled`|
|アプリケーショントラッキングが有効| `application_tracking_enabled`|
|カスタムイベント（`custom_events`）| `custom_events`［オブジェクトの配列］|
|イベントリスト（`event_list`）| `event_list`［オブジェクトの配列］|

### モバイル

|変数| 説明|
|---| ---|
|バンドルID| `app_rdns`を上書きします|
|バンドルバージョン|
|バンドル短縮バージョン| `app_version`を上書きします|

### イベント

|パラメータ| 説明 |
|---| ---|
|`fb_mobile_level_achieved`| レベル達成|
|`fb_mobile_activate_app`| アプリのアクティブ化|
|`fb_mobile_add_payment_info`| 支払い情報の追加|
|`fb_mobile_add_to_cart`| カートへの追加|
|`fb_mobile_add_to_wishlist`| ウィッシュリストへの追加|
|`fb_mobile_complete_registration`| 登録完了|
|`fb_mobile_tutorial_completion`| チュートリアル完了|
|`fb_mobile_initiated_checkout`| チェックアウト開始|
|`fb_mobile_purchase`| 購入|
|`fb_mobile_rate`| 評価|
|`fb_mobile_search`| 検索|
|`fb_mobile_spent_credits`| 使用済みクレジット|
|`fb_mobile_achievement_unlocked`| 実績のロック解除|
|`fb_mobile_content_view`| コンテンツ表示|
|カスタム| カスタム|

### パラメータ

|説明| パラメータ|
|---| ---|
|ログ時刻（`int`）| `_logTime`|
|Appバージョン | `_appVersion`|
|合計する値（`float`）| `_valueToSum`|
|コンテンツID（`string`）| `fb_content_id`|
|コンテンツタイプ（`string`）| `fb_content_type`|
|通貨（`string`）| `fb_currency`|
|説明（`string`）| `fb_description`|
|レベル（`string`）| `fb_level`|
|最大評価値（`int`）| `fb_max_rating_value`|
|アイテム数（`int`）| `fb_num_items`|
|支払い情報の有無（`1`または`0`）| `fb_payment_info_available`|
|登録方法（`string`）| `fb_registration_method`|
|検索文字列（`string`）| `fb_search_string`|
|成功（`1`または`0`）| `fb_success`|
|カスタム| カスタム|

### データ使用制限

|変数| 説明|
|---| ---|
| `lmt_data.use_ldu`（LDUを使用） | <ul><li>`true`の場合、Facebookのデータ使用制限オプションを使用します</li><li>`false`の場合、Facebookのデータ使用制限オプションを使用しません</li></ul> |
| `lmt_data.ldu_types.geolocate`（LDUで位置情報を特定） | <ul><li>`true`の場合、LDUはユーザーの位置情報を特定します。</li><li>`false`の場合、LDUはユーザーの位置情報を特定しません。**LDUを使用**が有効な場合、**LDUで位置情報を特定**もデフォルトで有効になります。</li></ul> |
| `lmt_data.ldu_types.california`（LDUの対象がカリフォルニア） | <ul><li>`true`の場合、テンプレート内で州と国にカリフォルニア固有の値を構成します。このオプションは、ユーザーがカリフォルニア州に所在し、データ使用制限の適用対象として処理する必要がある場合にのみ有効にしてください。</li><li>`false`の場合、テンプレート内でユーザーの州と国にカリフォルニア固有の値を構成しません。</li></ul> |