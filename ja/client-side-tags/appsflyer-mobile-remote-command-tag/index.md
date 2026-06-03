---
title: AppsFlyerモバイルリモートコマンドタグ
description: この記事では、Appsflyerモバイルリモートコマンドタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/appsflyer-mobile-remote-command-tag/
---
## タグのヒント

* 初回ロード時に、イベントリストにinitializeが見つからない場合や`b.lifecycle_type`がlaunchに構成されている場合、initializeとlaunchコマンドが自動的に送信されます。
* 適切なデータが提供された場合、ログインイベントは`setcustomerid`イベントも自動的に送信することができます。
* `af_content_id`は、`product_id`の最初のアイテムが利用可能で、値がマッピングされていない場合に自動的に使用されます。
* 次のEコマース拡張値をサポートします：
  * 注文ID
  * 注文合計
  * 注文通貨
  * 注文クーポンコード
  * IDリスト
  * 数量リスト
  * 価格リスト

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて]()を参照してください。

タグを追加する際に、以下の構成を構成します：

* **アプリID**：アプリケーションID。
* **SDK開発者キー**：ソフトウェア開発キット開発者のキー。
* **デバッグモードを有効にする**：デフォルトは`False`です。
* **購入自動追跡を有効にする**：デフォルトは`False`です。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へのデータ送信のプロセスです。詳細については、[データマッピングについて]()を参照してください。

利用可能なカテゴリは以下の通りです：

### 構成

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `command_name`  | 文字列 | コマンド名  |
|  `app_id`  | 文字列  |  アプリID|
|  `app_dev_key`  | 文字列 | アプリ開発キー |
|  `debug`  | ブール値 | デバッグ |
|  `disable_ad_tracking`  | ブール値 | 広告追跡を無効にする |
|  `disable_apple_ad_tracking`  | ブール値 | Apple広告追跡を無効にする |
|  `time_between_sessions`  | 整数 | セッション間の時間 |
|  `anonymize_user`  | ブール値 | ユーザーを匿名化する |
|  `collect_device_name`  | ブール値 | デバイス名を収集する |
|  `custom_data`  | [JSONオブジェクト] | カスタムデータ|
|  `resolve_deep_links`  | [文字列の配列] | ディープリンクを解決する |
|  `stop_tracking`  | ブール値 | トラッキングを停止する |
|  `customer_emails`  | [文字列の配列] | 顧客のメール |
|  `email_hash_type`  | 整数 |  メールハッシュタイプ|
|  `host`  | 文字列 | ホスト |
|  `host_prefix`  | 文字列 | ホストプレフィックス|

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------| :------------|
|  `af_achievement_id`  | 文字列 | 実績ID|
|  `af_adrev_ad_type`  | 文字列 | 広告タイプ |
|  `af_city`  | 文字列 | 市|
|  `af_class`  | 文字列 | クラス|
|  `af_content`  | [JSONエンコード文字列] | コンテンツ|
|  `af_content_id`  | 文字列 | コンテンツID |
|  `af_content_type`  | 文字列 | コンテンツタイプ |
|  `af_country`  | 文字列 | 国|
|  `af_customer_segment`  | 文字列 | 顧客セグメント|
|  `af_customer_user_id`  | 文字列 | 顧客ユーザーID |
|  `af_date_a`  | [文字列日付] | 日付A | 
|  `af_date_b`  | [文字列日付] | 日付B |
|  `af_deep_link`  | 文字列 | ディープリンク |
|  `af_departing_arrival_date`  | [文字列日付] | 出発到着日 | 
|  `af_departing_departure_date`  | [文字列日付] | 出発日 | 
|  `af_description`  | 文字列 | 説明 |
|  `af_destination_a`  | 文字列 | 目的地A |
|  `af_destination_b`  | 文字列 | 目的地B |
|  `af_destination_list`  | [文字列の配列] | 目的地リスト |
|  `af_event_end`  | 文字列 | イベント終了 |
|  `af_event_start`  | 文字列 | イベント開始 |
|  `af_hotel_score`  | 浮動小数点数 | ホテルスコア |
|  `af_lat`  | 整数 | 緯度 |
|  `af_level`  | 整数 | レベル |
|  `af_long`  | 整数 | 経度 |
|  `af_max_rating_value`  | 浮動小数点数 | 最大評価値 |
|  `af_new_version`  | 文字列 | 新バージョン |
|  `af_num_adults`  | 整数 | 大人の数 |
|  `af_num_children`  | 整数 | 子供の数|
|  `af_num_infants`  | 整数 | 幼児の数|
|  `af_old_version`  | 文字列 | 旧バージョン| 
|  `af_preferred_neighborhoods`  | [文字列の配列] | 優先地域 |
| `af_preferred_num_stops`  | [整数の配列] | 優先停留数 |
|  `af_preferred_price_range`  | [整数の配列] | 優先価格帯|
|  `af_preferred_star_ratings`  | [整数の配列] | 優先星評価 |
|  `af_rating_value`  | 浮動小数点数 | 評価値 |
|  `af_receipt_id`  | 文字列 | レシートID |
|  `af_region`  | 文字列 |地域|
|  `af_registration_method`  | 文字列 | 登録方法 |
|  `af_returning_arrival_date`  | [文字列日付] | 帰着到着日 |
|  `af_returning_departure_date`  | [文字列日付] | 帰着出発日 |
|  `af_review_text`  | 文字列 | レビューテキスト |
|  `af_score`  | 整数 | スコア |
|  `af_search_string`  | 文字列 | 検索文字列|
|  `af_success`  | ブール値 | 成功|
|  `af_suggested_destinations`  | [文字列の配列] | 提案された目的地 |
|  `af_suggested_hotels`  | [文字列の配列] | 提案されたホテル|
|  `af_travel_end`  | 文字列 | 旅行終了|
|  `af_travel_start`  | 文字列 | 旅行開始 |
|  `af_tutorial_id`  | 文字列 | チュートリアルID|
|  `af_user_score`  | 浮動小数点数 | ユーザースコア|
|  `af_validated`  | 文字列 | 検証済み|
|  `af_virtual_currency_name`  | 文字列 | 仮想通貨名 | 
|  `af_param_1`  | 文字列 |パラメータ1|
|   `af_param_2`  | 文字列 |パラメータ2|
|   `af_param_3`  | 文字列 |パラメータ3|
|   `af_param_4`  | 文字列 |パラメータ4|
|   `af_param_5`  | 文字列 |パラメータ5|
|   `af_param_6`  | 文字列 |パラメータ6|
|   `af_param_7`  | 文字列 |パラメータ7|
|  `af_param_8`  | 文字列 |パラメータ8|
|   `af_param_9`  | 文字列 |パラメータ9|
|   `af_param_10`  | 文字列 |パラメータ10|

### Eコマース

| 変数 | タイプ| 説明 |
|:---------|:------------|:------------|
| `order_id`  | 文字列 | 注文ID（`_corder`を上書き） 
 | `order_total`  | 文字列 | 注文合計/収益（`_ctotal`を上書き）
| `af_payment_info_available`  | ブール値 | 支払情報利用可能  |
| `af_purchase_currency`  | 文字列 | 購入通貨 |
 | `order_currency`  | 文字列 | 通貨（`_ccurrency`を上書き） |
 | `order_coupon_code`  | 文字列 | プロモコード/クーポンコード（`_cpromo`を上書き） |
| `product_id`  | 配列 |  商品ID/コンテンツIDリスト（`_cprod`を上書き） |
| `product_quantity` | 配列 | 数量リスト/数量（`_cquan`を上書き）  |
| `product_unit_price` | 配列 | 価格リスト/価格（`_cprice`を上書き）  |

### イベント
イベントをマッピングするには、[イベントマッピングの作成]()を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|   `initialize` | 初期化 |
|  `launch` | 起動 |
|   `tracklocation` | 位置追跡 |
|   `sethost` | ホスト構成 | 
|   `setuseremails` |ユーザーメール構成 |
|   `setcurrencycode` | 通貨コード構成 |
|  `setcustomerid` | 顧客ID構成 |
|  `disabletracking` | トラッキング無効化 |
| `resolvedeeplinkurls` | ディープリンクURL解決 |
| `achievelevel` | レベル達成  |
| `adclick` | 広告クリック |
|`adview` | 広告表示 |
|   `addpaymentinfo` | 支払情報追加 |
|  `addtocart` | カートに追加 |
|  `addtowishlist` | ウィッシュリストに追加 |
|  `completeregistration` | 登録完了 |
| `completetutorial` | チュートリアル完了 |
| `rate` |  評価 |
|  `starttrial` | トライアル開始 |
|   `subscribe` | 登録 |
|   `unlockachievement` | 実績解除 |
|  `spentcredits` | クレジット消費 |
|  `listview` | リスト表示 |
|   `share` | 共有 |
|  `invite` | 招待 |
|   `reengage` | 再エンゲージ |
|   `update` | 更新|
|  `login` |ログイン|
|   `search` | 検索|
|   `initiatecheckout` | チェックアウト開始 |
|  `purchase` | 購入 |
|  `viewedcontent` | コンテンツ閲覧 |
|  `travelbooking` | 旅行予約 |
| `customersegment` | 顧客セグメント |
### パラメータ
イベントをマッピングするには、[イベントマッピングの作成]()を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `command_name` | コマンド名 |
|  `app_id` | アプリID |
|  `app_dev_key` | アプリ開発キー | 
|   `debug` | デバッグ | 
|   `disable_ad_tracking` | 広告追跡を無効にする | 
|   `disable_apple_ad_tracking` | Appleの広告追跡を無効にする | 
|   `time_between_sessions` | セッション間の時間 |
|  `anonymize_user` | ユーザーを匿名化する | 
|  `collect_device_name` | デバイス名を収集する |
|   `custom_data` | カスタムデータ |
|   `resolve_deep_links` | ディープリンクを解決する |
|  `stop_tracking` | 追跡を停止する |
|   `customer_emails` | 顧客のメール |
|   `email_hash_type` | メールハッシュタイプ |
|  `host` | ホスト |
|   `host_prefix` | ホストプレフィックス |
|  `af_achievement_id` | 実績ID |
| `af_adrev_ad_type` | 広告タイプ |
|  `af_city` | 市 |
|   `af_class` | クラス |
|   `af_content` | コンテンツ |
| `af_content_id` | コンテンツID |
|  `af_content_type` | コンテンツタイプ |
|  `af_country` | 国 |
|  `af_customer_segment` | 顧客セグメント |
| `af_customer_user_id` | 顧客ユーザーID |
|   `af_date_a` | 日付A |
| `af_date_b` | 日付B |
|  `af_deep_link` | ディープリンク|
| `af_departing_arrival_date` | 出発到着日 |
|   `af_departing_departure_date` | 出発日 |
|  `af_description` | 説明 |
|  `af_destination_a` | 目的地A |
|   `af_destination_b` | 目的地B |
|   `af_destination_list` | 目的地リスト |
|   `af_event_end` | イベント終了 |
|   `af_event_start` | イベント開始 |
|  `af_hotel_score` |ホテルスコア |
|   `af_lat` |  緯度 |
|  `af_level` | レベル |
|  `af_long` | 経度 |
| `af_max_rating_value` | 最大評価値 |
| `af_new_version` | 新バージョン |
| `af_num_adults` | 大人の数 |
| `af_num_children` | 子供の数 |
| `af_num_infants` | 幼児の数 |
| `af_old_version` | 旧バージョン  |
| `af_preferred_neighborhoods` | 優先する近隣地域 |
| `af_preferred_num_stops` | 優先する停留所数 |
| `af_preferred_price_range` | 優先する価格帯 |
| `af_preferred_star_ratings` | 優先する星評価 |
| `af_rating_value` | 評価値 |
| `af_receipt_id` | レシートID |
| `af_region` | 地域 |
| `af_registration_method` | 登録方法 |
| `af_returning_arrival_date` | 帰着日 |
| `af_returning_departure_date` | 出発日 |
| `af_review_text` | レビューテキスト |
| `af_score` | スコア |
| `af_search_string` | 検索文字列 |
| `af_success` | 成功 |
| `af_suggested_destinations` | 提案された目的地 |
| `af_suggested_hotels` | 提案されたホテル |
| `af_travel_end` | 旅行終了 |
| `af_travel_start` | 旅行開始  |
| `af_tutorial_id` | チュートリアルID |
| `af_user_score` | ユーザースコア |
| `af_validated` | 検証済み |
| `af_virtual_currency_name` | 仮想通貨名 |
| `af_param_1` |パラメータ1 |
| `af_param_2` |パラメータ2 |
| `af_param_3` |パラメータ3 |
| `af_param_4` |パラメータ4 |
| `af_param_5` |パラメータ5 |
| `af_param_6` |パラメータ6 |
| `af_param_7` |パラメータ7 |
| `af_param_8` | パラメータ8 |
| `af_param_9` |  パラメータ9 |
| `af_param_10` | パラメータ10 (`af_param_10`) 
| `af_order_id` | 注文ID (Overrides `_corder`) 
| `af_revenue` | 注文合計/収益 (Overrides `_ctotal`)
| `af_payment_info_available` | 支払情報の有無 |
| `af_purchase_currency` | 購入通貨  |
| `af_currency` | 通貨 (Overrides `_ccurrency`) |
| `af_coupon_code` | プロモコード/クーポンコード  (Overrides `_cpromo`)  |
|  `af_content_list` | [配列] 製品ID/コンテンツIDのリスト (Overrides `_cprod`) |
| `af_quantity` | [配列]  数量のリスト/数量 (Overrides `_cquan`)  |
| `af_price` | [配列] 価格のリスト/価格 (Overrides `_cprice`) |
|  `custom` |カスタム |
