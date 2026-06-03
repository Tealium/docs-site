---
title: Facebookアプリアナリティクスタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでFacebookアプリアナリティクスタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/facebook-app-analytics-tag/
---
## タグのヒント

* Facebook開発者ドキュメント
  * [API v2.12](https://developers.facebook.com/docs/marketing-api/app-event-api/v2.12)
  * [アプリケーションアクティビティ](https://developers.facebook.com/docs/graph-api/reference/application/activities/)

* タグの構成
  * これらはダッシュボードで見つけることができます
  * APIバージョン
  * APP ID
  * APPトークン（APPシークレット）

## タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスし、Facebookアプリアナリティクスタグを追加します（[タグの追加方法についてはこちら]()を参照）。

タグを追加した後、以下の構成を行います：

* **アプリケーションID**：整数値（例：`123456`）
* **アクセストークン（アプリシークレット）**：整数値（例：`123456`）
* **イベント名**

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

|説明| パラメータ|
|---| ---|
|アプリID| `app_id`|
|アクセストークン| `access_token`|
|イベント名| `event_name`|
|広告主ID| `advertiser_id`|
|帰属| `attribution`|
|広告主トラッキング有効| `advertiser_tracking_enabled`|
|アプリケーショントラッキング有効| `application_tracking_enabled`|
|カスタムイベント (`custom_events`)| `custom_events` [オブジェクトの配列]|
|イベントリスト (`event_list`)| `event_list` [オブジェクトの配列]|

### モバイル

|変数| 説明|
|---| ---|
|バンドルID| `app_rdns`を上書き|
|バンドルバージョン|
|バンドルショートバージョン| `app_version`を上書き|

### イベント

|パラメータ| 説明 |
|---| ---|
|`fb_mobile_level_achieved`| レベル達成|
|`fb_mobile_activate_app`| アプリ活性化|
|`fb_mobile_add_payment_info`| 支払情報追加|
|`fb_mobile_add_to_cart`| カートに追加|
|`fb_mobile_add_to_wishlist`| ほしい物リストに追加|
|`fb_mobile_complete_registration`| 登録完了|
|`fb_mobile_tutorial_completion`| チュートリアル完了|
|`fb_mobile_initiated_checkout`| チェックアウト開始|
|`fb_mobile_purchase`| 購入|
|`fb_mobile_rate`| 評価|
|`fb_mobile_search`| 検索|
|`fb_mobile_spent_credits`| クレジット消費|
|`fb_mobile_achievement_unlocked`| 実績解除|
|`fb_mobile_content_view`| コンテンツ閲覧|
|カスタム| カスタム|

### パラメータ

|説明| パラメータ|
|---| ---|
|ログ時間 ( `int` )| `_logTime`|
|アプリバージョン | `_appVersion`|
|合計値 ( `float` )| `_valueToSum`|
|コンテンツID ( `string` )| `fb_content_id`|
|コンテンツタイプ ( `string` )| `fb_content_type`|
|通貨 ( `string` )| `fb_currency`|
|説明 ( `string` )| `fb_description`|
|レベル ( `string` )| `fb_level`|
|最大評価値 ( `int` )| `fb_max_rating_value`|
|アイテム数 ( `int` )| `fb_num_items`|
|支払情報有効 ( `1` または `0` )| `fb_payment_info_available`|
|登録方法 ( `string` )| `fb_registration_method`|
|検索文字列 ( `string` )| `fb_search_string`|
|成功( `1` または `0` )| `fb_success`|
|カスタム| カスタム|

### 限定データ使用

|変数| 説明|
|---| ---|
| `lmt_data.use_ldu` (LDU使用) |  &lt;ul&gt;&lt;li&gt;`true`の場合、Facebookの限定データ使用オプションを使用します&lt;/li&gt;&lt;li&gt;`false`の場合、Facebookの限定データ使用オプションを使用しません&lt;/li&gt;&lt;/ul&gt; |
| `lmt_data.ldu_types.geolocate` (LDUはジオロケートするべき) |  &lt;ul&gt;&lt;li&gt;`true`の場合、LDUはユーザーをジオロケートします。&lt;/li&gt;&lt;li&gt;`false`の場合、LDUはユーザーをジオロケートしません。**LDU使用**が有効な場合、**LDUはジオロケートするべき**もデフォルトで有効になります。&lt;/li&gt;&lt;/ul&gt; |
| `lmt_data.ldu_types.california` (LDUはカリフォルニア州) |  &lt;ul&gt;&lt;li&gt;`true`の場合、テンプレート内で州および国のカリフォルニア固有の値を構成します。ユーザーがカリフォルニアに位置しており、限定データ使用で処理する必要がある場合のみ、このオプションを有効にします。&lt;/li&gt;&lt;li&gt;`false`の場合、テンプレート内でユーザーの州および国のカリフォルニア固有の値を構成しません。&lt;/li&gt;&lt;/ul&gt; |
