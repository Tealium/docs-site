---
title: Firebase リモートコマンドタグ構成ガイド（モバイル）
url: https://docs.tealium.com/ja/client-side-tags/firebase-remote-command-tag/
---
## 概要

タグ管理で Firebase タグを実装するには、3つのコンポーネントが必要です。それぞれについて、ネイティブコードと Tealium の両方を変更する必要があります。まず、Firebase SDK をアプリに追加します。次に、Tealium SDK を使用して、リモートコマンドをネイティブコードに統合します。最後に、タグ管理で Firebase タグを追加します。Firebase がデータを受信するには、これら3つの手順をすべて実行する必要があります。

## タグに関するヒント

* `initiateconversionmeasurement` メソッド（iOS のみ）は、次の4つのパラメータをサポートしていますが、渡すことができるのはそのうち1つだけです。
  * `param_email_address`
  * `param_phone_number`
  * `param_hashed_email_address`
  * `param_hashed_phone_number`
* [Firebase のドキュメント](https://firebase.google.com/docs/guides)の説明に従って、ハッシュ化されたパラメータを正規化してください。

## ネイティブコードの構成

* 手順1 – Firebase SDK をネイティブアプリに追加します。
* 手順2 – Tealium SDK をネイティブアプリに追加します。
* 手順3 – リモートコマンドクラスをネイティブアプリに組み込みます。

すべてのライブラリについて、使用する前に Firebase Analytics リモートコマンドを登録する必要があります。この登録は、ライブラリの初期化時に行ってください。使用しているモバイルプラットフォームに応じてリモートコマンドを実装するには、[ガイドに従ってください](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/)。

## タグ管理の構成

### 手順1 – Firebase タグを追加する

Firebase タグは、Tealium モバイルライブラリに登録したカスタムネイティブコードブロックをトリガーするために必要な API の実装を含む特殊なタグです。このタグはタグマーケットプレイスで提供されており、ネイティブアプリ構成の「手順3」と通信します。

### 仕組み

Tealium イベント（ビューまたはイベント）はネイティブコードによってトリガーされ、その後、WebView 内の `utag.js` ファイルに取り込まれます。Firebase タグと関連する拡張機能がイベントを確認し、ネイティブコードに追加されたリモートコマンドへ Firebase イベントを送信します。リモートコマンドはタグからリクエストを受け取り、Firebase タグによって収集できるようにイベントを整形して送信します。

![](https://docs.tealium.com/images/client-side-tags/howitworks-firebasetag.jpg)

### 手順2 – タグ構成を指定する

構成できる唯一のオプションは、デバッグモードを有効にするかどうかです。このオプションを有効にする必要があるかどうかは、開発者が判断してください。デフォルト構成は「False」です。

### 手順3 – マッピングを追加する

#### 構成

このタグには、次のマッピングが必要です。

* セッションタイムアウト（秒）
* 最小セッション時間（秒）
* Firebase ログレベル
* 画面名
* コマンド名
* Firebase イベント

これらは静的な値として構成することも、拡張機能を使用して動的に構成することもできます。

|変数|説明|
|---|---|
|`firebase_session_timeout_seconds`| <ul><li>文字列形式の整数</li></ul> |
|`firebase_session_minimum_seconds`| <ul><li>文字列形式の整数</li></ul> |
|`firebase_analytics_enabled`| <ul><li>文字列形式のブール値</li></ul> |
|`firebase_log_level`| <ul><li>文字列</li></ul>|
|`firebase_event_name`| <ul><li>文字列</li></ul> |
|`firebase_event_params`| <ul><li>JSON</li></ul> |
|`firebase_screen_name`| <ul><li>文字列</li></ul> |
|`firebase_screen_class`| <ul><li>文字列</li></ul> |
|`firebase_property_name`| <ul><li>文字列</li></ul> |
|`firebase_property_value`| <ul><li>文字列</li></ul> |
|`firebase_user_id`| <ul><li>文字列</li></ul> |
|`command_name`| <ul><li>文字列</li></ul> |

#### 自動イベント

使用されるイベントの一部は Firebase SDK によって自動的に収集されるため、Tealium Firebase タグを使用して構成する必要はありません。これらのイベントの一覧については、[こちらをクリックしてください](https://support.google.com/firebase/answer/6317485?hl=en)。

#### 標準イベント

イベント名は、取得する必要があるアプリ内イベント（カートイベント、検索イベント、決済イベントなど）です。以下は、Firebase SDK で利用できる標準イベントの一覧です。対象のイベントが一覧にない場合は、`logEvent` カスタムイベントを使用して送信できます。

* `config`
* `event_add_payment_info`
* `event_add_to_cart`
* `event_add_to_wishlist`
* `event_app_open`
* `event_begin_checkout`
* `event_campaign_details`
* `event_checkout_progress`
* `event_earn_virtual_currency`
* `event_ecommerce_purchase`
* `event_generate_lead`
* `event_join_group`
* `event_level_end`
* `event_level_start`
* `event_level_up`
* `event_login`
* `event_post_score`
* `event_present_offer`
* `event_purchase_refund`
* `event_remove_cart`
* `event_search`
* `event_select_content`
* `event_set_checkout_option`
* `event_share`
* `event_signup`
* `event_spend_virtual_currency`
* `event_tutorial_begin`
* `event_tutorial_complete`
* `event_unlock_achievement`
* `event_view_item`
* `event_view_item_list`
* `event_view_search_results`
* `logEvent`
* `resetData`
* `setScreenName`
* `setUserId`
* `setUserProperty`
* `initiateconversionmeasurement`（iOS のみ）

Firebase イベントは、他のタグの場合と同じようにマッピングします。値はデータレイヤーから取得することも、拡張機能を使用して構成することもできます。その後、次のようにタグへマッピングします。

![](https://docs.tealium.com/images/client-side-tags/screen-shot-2020-10-02-at-9.07.39-am-markup.jpg)

#### カスタムイベント

送信するイベントがデフォルトイベントの一覧に含まれていない場合は、イベント名のカスタム値を指定した `logEvent` イベントを送信する必要があります。

1. 変数の値を `logEvent` イベントにマッピングします。
1. `logEvent` イベントとともにイベント名を送信するためのパラメータを追加します。

**![](https://docs.tealium.com/images/client-side-tags/screen-shot-2020-10-02-at-9.15.36-am-markup.jpg)**
#### 標準パラメータ

イベントパラメータはイベントとともに送信され、以下のリストにあるパラメータへマッピングできます。パラメータは次の2つの方法でマッピングできます。

* 任意のイベントとともに送信される標準パラメータとして
* 指定したイベントでのみ送信されるイベントパラメータとして

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `param_achievement_id` | `String` | 実績ID。 |
| `param_ad_network_click_id` | `String` | 広告ネットワークのクリックID。 |
| `param_affiliation` | `String` | アフィリエーション。 |
| `param_cp1` | `String` | CP1。|
| `param_campaign` | `String` | キャンペーン。 |
| `param_character` | `String` | キャラクター。 |
| `param_content` | `String` | コンテンツ。 |
| `param_content_type` | `String` | コンテンツタイプ。 |
| `param_coupon` | `String` | クーポン。 |
| `param_creative_name` | `String` | クリエイティブ名。 |
| `param_creative_slot` | `String` | クリエイティブスロット。 |
| `param_currency` | `String` | 通貨。 |
| `param_destination` | `String` | 目的地。 |
| `param_end_date` | `String` | 終了日。 |
| `param_flight_number` | `String` | フライト番号。 |
| `param_group_id` | `String` | グループID。 |
| `param_index` | `String` | インデックス。 |
| `param_item_brand` | `String` | アイテムのブランド。 |
| `param_item_category` | `String` | アイテムのカテゴリー。 |
| `param_item_id` | `String` | アイテムID。 |
| `param_item_list` | `String` | アイテムリスト。 |
| `param_item_name` | `String` | アイテム名。 |
| `param_item_variant` | `String` | アイテムのバリエーション。 |
| `param_level` | `Long` | レベル。 |
| `param_location` | `Long` | 場所。 |
| `param_medium` | `String` | メディア。 |
| `param_number_nights` | `Long` | 宿泊数。 |
| `param_number_pax` | `Long` | 乗客数。 |
| `param_number_rooms` | `Long` | 部屋数。 |
| `param_origin` | `String` | 出発地。 |
| `param_price` | `Double` | 価格。 |
| `param_quantity` | `Long` | 数量。 |
| `param_screen_name` | `String` | 画面名。 |
| `param_screen_class` | `String` | 画面クラス。 |
| `param_score` | `Long` | スコア。 |
| `param_search_term` | `String` | 検索語句。 |
| `param_shipping` | `Double` | 送料。 |
| `param_method` | `String` | 方法。 |
| `param_source` | `String` | ソース。 |
| `param_travel_class` | `String` | 旅行クラス。 |
| `param_virtual_currency_name` | `String` | 仮想通貨名。 |
| `param_start_date` | `String` | 開始日。 |
| `param_term` | `String` | キーワード。 |
| `param_tax` | `Double` | 税金。 |
| `param_transaction_id` | `String` | トランザクションID。 |
| `param_value` | `Long or Double` | 値。 |
| `param_level_name` | `String` | レベル名。 |
| `param_success` | `String` | 成功。 |
| `param_ad_format` | `String` | 広告フォーマット。 |
| `param_ad_platform` | `String` | 広告プラットフォーム。 |
| `param_ad_source` | `String` | 広告ソース。 |
| `param_ad_unit_name` | `String` | 広告ユニット名。 |
| `param_campaign_id` | `String` | キャンペーンID。 |
| `param_creative_format` | `String` | クリエイティブフォーマット。 |
| `param_discount` | `String` | 割引。 |
| `param_extend_session` | `String` | セッションの延長。 |
| `param_item_category2` | `String` | アイテムカテゴリー2。 |
| `param_item_category3` | `String` | アイテムカテゴリー3。 |
| `param_item_category4` | `String` | アイテムカテゴリー4。 |
| `param_item_category5` | `String` | アイテムカテゴリー5。 |
| `param_item_list_id` | `String` | アイテムリストID。 |
| `param_item_list_name` | `String` | アイテムリスト名。 |
| `param_items` | `Array` | アイテム。 |
| `param_level_name` | `String` | レベル名。 |
| `param_location_id` | `String` | 場所ID |
| `param_marketing_tactic` | `String` | マーケティング施策。 |
| `param_payment_type` | `String` | 支払い方法。 |
| `param_promotion_id` | `String` | プロモーションID。 |
| `param_promotion_name` | `String` | プロモーション名。 |
| `param_shipping_tier` | `String` | 配送区分。 |
| `param_source_platform` | `String` | ソースプラットフォーム。 |
| `param_travel_class` | `String` | 旅行クラス。 |
| `param_virtual_currency_name` | `String` | 仮想通貨名。 |
| `param_user_signup_method` | `String` | ユーザー登録方法。 |
| `param_user_allow_ad_personalization_signals` | `String` | ユーザーによる広告パーソナライズシグナルの許可。 |
| `param_email_address` | `String` | メールアドレス。 |
| `param_phone_number` | `String` | 電話番号。 |
| `param_hashed_email_address` | `String` | ハッシュ化されたメールアドレス。 |
| `param_hashed_phone_number` | `String` | ハッシュ化された電話番号。 |

#### Eコマース

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文`ID`（`_corder`を上書き）。 |
| `order_total` | `Long or Double` | 注文合計（`_ctotal`を上書き）。 |
| `order_shipping` | `Double` | 送料（`_cship`を上書き）。 |
| `order_tax` | `Double` | 税額（`_ctax`を上書き）。 |
| `order_currency` | `String` | 通貨（`_ccurrency`を上書き）。 |
| `order_coupon_code` | `String` | プロモーションコード（`_cpromo`を上書き）。 |
| `product_id` | `Array` | 商品IDのリスト（`_cprod`を上書き）。 |
| `product_name` | `Array` | 名前のリスト（`_cprodname`を上書き）。 |
| `product_brand` | `Array` | ブランドのリスト（`_cbrand`を上書き）。 |
| `product_category` | `Array` | カテゴリーのリスト（`_ccat`を上書き）。 |
| `product_quantity` | `Array` | 数量のリスト（`_cquan`を上書き）。 |
| `product_unit_price` | `Array` | 価格のリスト（`_cprice`を上書き）。 |
| `param_item_list` | `Array` | 表示リストの一覧。 |
| `param_item_variant` | `Array` | バリエーションのリスト。 |
| `param_index` | `Array` | インデックスのリスト。 |

#### 同意構成

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `ad_storage` | `String` | 広告保存。 |
| `analytics_storage` | `String` | アナリティクス保存。 |
| `ad_user_data` | `String` | 広告ユーザーデータ。 |
| `ad_personalization` | `String` | 広告のパーソナライズ。 |

#### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `config` | 構成。 |
| `setScreenName` | 画面名を構成。 |
| `setUserProperty` | ユーザープロパティを構成。 |
| `setUserId` | ユーザーIDを構成。 |
| `logEvent` | イベントを記録。 |
| `resetData` | データをリセット。 |
| `event_add_payment_info` | 支払い情報を追加。 |
| `event_add_to_cart` | カートに追加。 |
| `event_add_to_wishlist` | ほしいものリストに追加。 |
| `event_app_open` | アプリを起動。 |
| `event_begin_checkout` | 購入手続きを開始。 |
| `event_campaign_details` | キャンペーンの詳細。 |
| `event_earn_virtual_currency` | 仮想通貨を獲得。 |
| `event_generate_lead` | リードを獲得。 |
| `event_join_group` | グループに参加。 |
| `event_level_up` | レベルアップ。 |
| `event_level_start` | レベルを開始。 |
| `event_level_end` | レベルを終了。 |
| `event_login` | ログイン。 |
| `event_post_score` | スコアを送信。 |
| `event_remove_cart` | カートから削除。 |
| `event_screen_view` | 画面を表示。 |
| `event_search` | 検索。 |
| `event_select_content` | コンテンツを選択。 |
| `event_share` | 共有。 |
| `event_signup` | 登録。 |
| `event_spend_virtual_currency` | 仮想通貨を使用。 |
| `event_tutorial_begin` | チュートリアルを開始。 |
| `event_tutorial_complete` | チュートリアルを終了。 |
| `event_unlock_achievement` | 実績を解除。 |
| `event_view_item` | アイテムを表示。 |
| `event_view_item_list` | アイテムリストを表示。 |
| `event_view_search_results` | 検索結果を表示。 |
| `event_ad_impression` | 広告インプレッション。 |
| `event_add_shipping_info` | 配送情報を追加。 |
| `purchase` | 購入。 |
| `event_refund` | 払い戻し。 |
| `event_select_item` | アイテムを選択。 |
| `event_select_promotion` | プロモーションを選択。 |
| `event_view_cart` | カートを表示。 |
| `event_view_promotion` | プロモーションを表示。 |
| `initiateconversionmeasurement` | コンバージョン測定を開始。 |
| `resetdata` | データをリセット。 |
| `setConsent` | 同意を構成。 |
#### パラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `param_ad_format` | 広告フォーマット。 |
| `param_ad_platform` | 広告プラットフォーム。 |
| `param_ad_source` | 広告ソース。 |
| `param_ad_unit_name` | 広告ユニット名。 |
| `param_campaign_id` | キャンペーン ID。 |
| `param_creative_format` | クリエイティブフォーマット。 |
| `param_discount` | 割引。 |
| `param_extend_session` | セッションの延長。 |
| `param_item_category2` | 商品カテゴリー 2。 |
| `param_item_category3` | 商品カテゴリー 3。 |
| `param_item_category4` | 商品カテゴリー 4。 |
| `param_item_category5` | 商品カテゴリー 5。 |
| `param_item_list_id` | 商品リスト ID。 |
| `param_item_list_name` | 商品リスト名。 |
| `param_items` | 商品。 |
| `param_level_name` | レベル名。 |
| `param_location_id` | ロケーション ID。 |
| `param_marketing_tactic` | マーケティング戦術。 |
| `param_payment_type` | 支払い方法。 |
| `param_promotion_id` | プロモーション ID。 |
| `param_promotion_name` | プロモーション名。 |
| `param_shipping_tier` | 配送区分。 |
| `param_source_platform` | ソースプラットフォーム。 |
| `param_travel_class` | 旅行クラス。 |
| `param_virtual_currency_name` | 仮想通貨名。 |
| `param_user_signup_method` | ユーザー登録方法。 |
| `param_email_address` | メールアドレス。 |
| `param_phone_number` | 電話番号。 |
| `param_hashed_email_address` | ハッシュ化されたメールアドレス。 |
| `param_hashed_phone_number` | ハッシュ化された電話番号。 |
| `param_user_allow_ad_personalization_signals` | ユーザーによる広告パーソナライズシグナルの許可。 |
| `ad_storage` | 広告保存。 |
| `analytics_storage` | アナリティクス保存。 |
| `ad_user_data` | 広告ユーザーデータ。 |
| `ad_personalization` | 広告のパーソナライズ。 |

#### カスタムパラメータ

使用するパラメータが上記の表にない場合は、カスタムパラメータをイベントとともに送信する必要があります。イベントにカスタムパラメータを追加する場合、それらは標準イベントまたはカスタムイベントとともに送信され、JSON 形式でなければならないことに注意してください。マッピングされた変数の値は、JavaScript 拡張機能を使用して構成する必要があります。複数のイベントは、次の図のようにフォーマットできます。

![](https://docs.tealium.com/images/client-side-tags/screen-shot-2020-10-02-at-10.54.39-am.png)

カスタムパラメータを送信するためのマッピングは、次のように構成します。

![](https://docs.tealium.com/images/client-side-tags/screen-shot-2020-10-02-at-10.57.00-am.png)

## ヒント

Firebase Remote Command タグを構成する際は、次の点に留意してください。

* イベントリストに config コマンドが見つからない場合、初回読み込み時に自動的に送信されます。
* 適切なデータが提供されている場合（変数が **ユーザー ID** にマッピングされている場合）、`event_login` イベントと `event_signup` イベントは、`setUserId` イベントと `setUserProperty` イベントを自動的に送信します。
* 適切なデータが提供されている場合（変数が **画面名** にマッピングされている場合）、`event_view_item_list`、`event_view_item`、`event_ecommerce_purchase`、`event_begin_checkout` は、`setScreenName` イベントを自動的に送信できます。
* 単一パラメータまたは e コマース配列のいずれか一方のみを使用し、両方は使用しないでください。

## Firebase に関する注意事項

Firebase は Google Analytics と同じものではなく、用語や構成方法がまったく異なります。変数とマッピングは一対一では対応しないため、Firebase にはカスタムディメンションが含まれていません。パラメータがカスタムディメンションの代わりとなるため、それに応じて使用してください。カスタムパラメータが必要な場合は、Firebase 内で構成できます。

A/B テストのパラメータは Firebase に保存され、Tealium からはアクセスできません。A/B テストデータを Tealium 内で使用する必要がある場合は、BigQuery を使用して Firebase から無料でデータをエクスポートできます。その後、データを Tealium のサーバーサイド製品にインポートし、コネクタやオーディエンスで使用できます。

## リソース

[Tealium Firebase Remote Command インテグレーション](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/)<br>
[Firebase Remote Command の例 – iOS（GitHub）](https://github.com/Tealium/tealium-ios-firebase-remote-command)<br>
[Firebase Remote Command の例 – Android（GitHub）](https://github.com/Tealium/tealium-android-firebase-remote-command)<br>
[Google Firebase ガイド](https://firebase.google.com/docs/guides)<br>
[自動的に収集されるイベント – Firebase](https://support.google.com/firebase/answer/6317485?hl=en)