---
title: モバイル用Firebaseリモートコマンドタグ構成ガイド
description: Tealium iQでFirebaseタグを実装するには、ネイティブコードとTealiumの両方に変更を加える3つのコンポーネントが必要です。まず、アプリにFirebase SDKを追加します。次に、Tealium SDKを使用してネイティブコードにリモートコマンドを統合します。最後に、Tealium iQにFirebaseタグを追加します。Firebaseがデータを受信するには、これら3つのステップが必要です。
url: https://docs.tealium.com/ja/client-side-tags/firebase-remote-command-tag/
---
## 概要

Tealium iQでFirebaseタグを実装するには、ネイティブコードとTealiumの両方に変更を加える3つのコンポーネントが必要です。まず、アプリにFirebase SDKを追加します。次に、Tealium SDKを使用してネイティブコードにリモートコマンドを統合します。最後に、Tealium iQにFirebaseタグを追加します。これら3つのステップがすべて必要です。

## タグのヒント

* `initiateconversionmeasurement` メソッド（iOSのみ）は以下の4つのパラメータをサポートしていますが、1つだけを渡すことができます：
  * `param_email_address`
  * `param_phone_number`
  * `param_hashed_email_address`
  * `param_hashed_phone_number`
* ハッシュ化されたパラメータは、[Firebaseのドキュメント](https://firebase.google.com/docs/guides)に記載されているように正規化します。

## ネイティブコードの構成

* ステップ1 – ネイティブアプリにFirebase SDKを追加します。
* ステップ2 – ネイティブアプリにTealium SDKを追加します。
* ステップ3 – ネイティブアプリにリモートコマンドクラスを含めます。

すべてのライブラリについて、ライブラリを使用する前にFirebase Analyticsリモートコマンドを登録する必要があります。これはライブラリを初期化するときに行うべきです。[ガイドに従って](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/)、使用しているモバイルプラットフォームに基づいてリモートコマンドを実装します。

## Tealium iQの構成

### ステップ1 – Firebaseタグを追加

Firebaseタグは、Tealiumモバイルライブラリに登録したカスタムネイティブコードブロックをトリガーするために必要なAPIの実装を含む特別なタグです。このタグはタグマーケットプレイスで利用可能であり、ネイティブアプリ構成の「ステップ3」と通信します。

### 動作方法

Tealiumイベント（ビューまたはイベント）はネイティブコードによってトリガーされ、その後`utag.js`ファイルによってウェブビューで取り込まれます。Firebaseタグと関連する拡張機能はイベントをレビューし、リモートコマンドにFirebaseイベントを送信します。リモートコマンドはタグからのリクエストを受け取り、イベントをフォーマットして送信し、Firebaseタグによって収集されます。

![](/images/client-side-tags/howitworks-firebasetag.jpg)

### ステップ2 – タグ構成を構成

構成のオプションは、デバッグモードを有効にするかどうかのみです。開発者がこのオプションを有効にする必要があるかどうかを決定する必要があります。デフォルト構成は「False」です。

### ステップ3 – マッピングを追加

#### 構成

このタグには以下のマッピングが必要です：

* セッションタイムアウト（秒）
* セッション最小（秒）
* Firebaseログレベル
* 画面名
* コマンド名
* Firebaseイベント

これらは静的値として構成することも、拡張機能を使用して動的に構成することもできます。

|変数| 説明|
|---| ---|
|`firebase_session_timeout_seconds`|  &lt;ul&gt;&lt;li&gt;文字列としての整数&lt;/li&gt;&lt;/ul&gt; |
|`firebase_session_minimum_seconds`|  &lt;ul&gt;&lt;li&gt;文字列としての整数&lt;/li&gt;&lt;/ul&gt; |
|`firebase_analytics_enabled`|  &lt;ul&gt;&lt;li&gt;文字列としてのブール値&lt;/li&gt;&lt;/ul&gt; |
|`firebase_log_level`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt;|
|`firebase_event_name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`firebase_event_params`|  &lt;ul&gt;&lt;li&gt;JSON&lt;/li&gt;&lt;/ul&gt; |
|`firebase_screen_name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`firebase_screen_class`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`firebase_property_name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`firebase_property_value`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`firebase_user_id`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |
|`command_name`|  &lt;ul&gt;&lt;li&gt;文字列&lt;/li&gt;&lt;/ul&gt; |

#### 自動イベント

Firebase SDKによって自動的に収集されるイベントの一部は、Tealium Firebaseタグを使用して構成する必要はありません。これらのイベントのリストについては、[こちらをクリックしてください](https://support.google.com/firebase/answer/6317485?hl=en)。

#### 標準イベント

イベント名はアプリ内で発生するイベントであり、キャプチャする必要があります（カートイベント、検索イベント、支払いイベントなど）。以下はFirebase SDKを通じて利用可能な標準イベントのリストです。イベントがリストにない場合は、カスタムイベントとして`logEvent`を使用して送信することができます。

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
* `initiateconversionmeasurement` (iOSのみ)

Firebaseイベントは他のタグと同様にマッピングされます。値はデータレイヤーから取得するか、拡張機能を通じて構成され、次の方法でタグにマッピングされます：

![](/images/client-side-tags/screen-shot-2020-10-02-at-9.07.39-am-markup.jpg)

#### カスタムイベント

デフォルトのイベントリストに含まれていないイベントを送信する場合は、イベント名を添付して`logEvent`イベントを送信する必要があります。

1. 変数値を`logEvent`イベントにマッピングします。
1. `logEvent`イベントでイベント名を送信するためのパラメータを追加します。

**![](/images/client-side-tags/screen-shot-2020-10-02-at-9.15.36-am-markup.jpg)**
#### 標準パラメータ

イベントと共に送信されるイベントパラメータは、以下のリストにあるパラメータにマッピングできます。パラメータのマッピングは2つの方法で行うことができます：

* 任意のイベントに送信される標準パラメータとして
* 特定のイベントのみに送信されるイベントパラメータとして

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `param_achievement_id` | `String` | 実績ID。 |
| `param_ad_network_click_id` | `String` | 広告ネットワーククリックID。 |
| `param_affiliation` | `String` | 所属。 |
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
| `param_item_brand` | `String` | アイテムブランド。 |
| `param_item_category` | `String` | アイテムカテゴリ。 |
| `param_item_id` | `String` | アイテムID。 |
| `param_item_list` | `String` | アイテムリスト。 |
| `param_item_name` | `String` | アイテム名。 |
| `param_item_variant` | `String` | アイテムバリアント。 |
| `param_level` | `Long` | レベル。 |
| `param_location` | `Long` | 位置。 |
| `param_medium` | `String` | ミディアム。 |
| `param_number_nights` | `Long` | 宿泊数。 |
| `param_number_pax` | `Long` | 乗客数。 |
| `param_number_rooms` | `Long` | 部屋数。 |
| `param_origin` | `String` | 発地。 |
| `param_price` | `Double` | 価格。 |
| `param_quantity` | `Long` | 数量。 |
| `param_screen_name` | `String` | スクリーン名。 |
| `param_screen_class` | `String` | スクリーンクラス。 |
| `param_score` | `Long` | スコア。 |
| `param_search_term` | `String` | 検索語。 |
| `param_shipping` | `Double` | 配送料。 |
| `param_method` | `String` | 方法。 |
| `param_source` | `String` | ソース。 |
| `param_travel_class` | `String` | 旅行クラス。 |
| `param_virtual_currency_name` | `String` | 仮想通貨名。 |
| `param_start_date` | `String` | 開始日。 |
| `param_term` | `String` | 期間。 |
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
| `param_extend_session` | `String` | セッション延長。 |
| `param_item_category2` | `String` | アイテムカテゴリ2。 |
| `param_item_category3` | `String` | アイテムカテゴリ3。 |
| `param_item_category4` | `String` | アイテムカテゴリ4。 |
| `param_item_category5` | `String` | アイテムカテゴリ5。 |
| `param_item_list_id` | `String` | アイテムリストID。 |
| `param_item_list_name` | `String` | アイテムリスト名。 |
| `param_items` | `Array` | アイテム。 |
| `param_level_name` | `String` | レベル名。 |
| `param_location_id` | `String` | 位置ID |
| `param_marketing_tactic` | `String` | マーケティング戦術。 |
| `param_payment_type` | `String` | 支払いタイプ。 |
| `param_promotion_id` | `String` | プロモーションID。 |
| `param_promotion_name` | `String` | プロモーション名。 |
| `param_shipping_tier` | `String` | 配送層。 |
| `param_source_platform` | `String` | ソースプラットフォーム。 |
| `param_travel_class` | `String` | 旅行クラス。 |
| `param_virtual_currency_name` | `String` | 仮想通貨名。 |
| `param_user_signup_method` | `String` | ユーザー登録方法。 |
| `param_user_allow_ad_personalization_signals` | `String` | ユーザーが広告のパーソナライゼーション信号を許可。 |
| `param_email_address` | `String` | メールアドレス。 |
| `param_phone_number` | `String` | 電話番号。 |
| `param_hashed_email_address` | `String` | ハッシュ化されたメールアドレス。 |
| `param_hashed_phone_number` | `String` | ハッシュ化された電話番号。 |

#### E-Commerce

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | `String` | 注文`ID`（`_corder`を上書き）。 |
| `order_total` | `Long or Double` | 注文合計（`_ctotal`を上書き）。 |
| `order_shipping` | `Double` | 配送料（`_cship`を上書き）。 |
| `order_tax` | `Double` | 税金（`_ctax`を上書き）。 |
| `order_currency` | `String` | 通貨（`_ccurrency`を上書き）。 |
| `order_coupon_code` | `String` | プロモコード（`_cpromo`を上書き）。 |
| `product_id` | `Array` | 製品IDのリスト（`_cprod`を上書き）。 |
| `product_name` | `Array` | 名前のリスト（`_cprodname`を上書き）。 |
| `product_brand` | `Array` | ブランドのリスト（`_cbrand`を上書き）。 |
| `product_category` | `Array` | カテゴリのリスト（`_ccat`を上書き）。 |
| `product_quantity` | `Array` | 数量のリスト（`_cquan`を上書き）。 |
| `product_unit_price` | `Array` | 価格のリスト（`_cprice`を上書き）。 |
| `param_item_list` | `Array` | プレゼンテーションリストのリスト。 |
| `param_item_variant` | `Array` | バリアントのリスト。 |
| `param_index` | `Array` | インデックスのリスト。 |

#### 同意構成

| 変数 | タイプ/値 | 説明 |
|:---------|:-----|:------------|
| `ad_storage` | `String` | 広告保存。 |
| `analytics_storage` | `String` | 分析保存。 |
| `ad_user_data` | `String` | 広告ユーザーデータ。 |
| `ad_personalization` | `String` | 広告パーソナライゼーション。 |

#### イベント

イベントのマッピングについては、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `config` | 構成。 |
| `setScreenName` | スクリーン名を構成。 |
| `setUserProperty` | ユーザープロパティを構成。 |
| `setUserId` | ユーザーIDを構成。 |
| `logEvent` | イベントを記録。 |
| `resetData` | データをリセット。 |
| `event_add_payment_info` | 支払情報を追加。 |
| `event_add_to_cart` | カートに追加。 |
| `event_add_to_wishlist` | ウィッシュリストに追加。 |
| `event_app_open` | アプリを開く。 |
| `event_begin_checkout` | チェックアウトを開始。 |
| `event_campaign_details` | キャンペーンの詳細。 |
| `event_earn_virtual_currency` | 仮想通貨を獲得。 |
| `event_generate_lead` | リードを生成。 |
| `event_join_group` | グループに参加。 |
| `event_level_up` | レベルアップ。 |
| `event_level_start` | レベル開始。 |
| `event_level_end` | レベル終了。 |
| `event_login` | ログイン。 |
| `event_post_score` | スコアを投稿。 |
| `event_remove_cart` | カートから削除。 |
| `event_screen_view` | スクリーンビュー。 |
| `event_search` | 検索。 |
| `event_select_content` | コンテンツを選択。 |
| `event_share` | 共有。 |
| `event_signup` | サインアップ。 |
| `event_spend_virtual_currency` | 仮想通貨を使用。 |
| `event_tutorial_begin` | チュートリアル開始。 |
| `event_tutorial_complete` | チュートリアル終了。 |
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
| `initiateconversionmeasurement` | 変換測定を開始。 |
| `resetdata` | データをリセット。 |
| `setConsent` | 同意を構成。 |
#### パラメータ

イベントをマッピングするには、[イベントマッピングの作成](/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| イベント | 説明 |
|:------|:------------|
| `param_ad_format` | 広告フォーマット。 |
| `param_ad_platform` | 広告プラットフォーム。 |
| `param_ad_source` | 広告ソース。 |
| `param_ad_unit_name` | 広告ユニット名。 |
| `param_campaign_id` | キャンペーンID。 |
| `param_creative_format` | クリエイティブフォーマット。 |
| `param_discount` | 割引。 |
| `param_extend_session` | セッション延長。 |
| `param_item_category2` | アイテムカテゴリー2。 |
| `param_item_category3` | アイテムカテゴリー3。 |
| `param_item_category4` | アイテムカテゴリー4。 |
| `param_item_category5` | アイテムカテゴリー5。 |
| `param_item_list_id` | アイテムリストID。 |
| `param_item_list_name` | アイテムリスト名。 |
| `param_items` | アイテム。 |
| `param_level_name` | レベル名。 |
| `param_location_id` | ロケーションID。 |
| `param_marketing_tactic` | マーケティング戦術。 |
| `param_payment_type` | 支払いタイプ。 |
| `param_promotion_id` | プロモーションID。 |
| `param_promotion_name` | プロモーション名。 |
| `param_shipping_tier` | 配送層。 |
| `param_source_platform` | ソースプラットフォーム。 |
| `param_travel_class` | 旅行クラス。 |
| `param_virtual_currency_name` | 仮想通貨名。 |
| `param_user_signup_method` | ユーザー登録方法。 |
| `param_email_address` | メールアドレス。 |
| `param_phone_number` | 電話番号。 |
| `param_hashed_email_address` | ハッシュ化されたメールアドレス。 |
| `param_hashed_phone_number` | ハッシュ化された電話番号。 |
| `param_user_allow_ad_personalization_signals` | ユーザーが広告のパーソナライゼーション信号を許可。 |
| `ad_storage` | 広告保存。 |
| `analytics_storage` | アナリティクス保存。 |
| `ad_user_data` | 広告ユーザーデータ。 |
| `ad_personalization` | 広告パーソナライゼーション。 |

#### カスタムパラメータ

上記の表にパラメータがない場合、イベントにカスタムパラメータを送信する必要があります。イベント（標準またはカスタム）にカスタムパラメータを追加する際には、それらがイベントと共に送信され、JSON形式である必要があります。マッピングされた変数の値は、Javascript拡張を使用して構成する必要があります。複数のイベントは、以下の図に示すようにフォーマットできます：

![](/images/client-side-tags/screen-shot-2020-10-02-at-10.54.39-am.png)

カスタムパラメータを送信するためのマッピングは、以下に示すように構成されます。

![](/images/client-side-tags/screen-shot-2020-10-02-at-10.57.00-am.png)

## ヒント

Firebase Remote Command Tagを構成する際に留意すべきいくつかの項目です。

* 初回ロード時にイベントリストにない場合、configコマンドが自動的に送信されます。
* 適切なデータが提供されている場合（**ユーザーID**にマッピングされた変数）、`event_login`および`event_signup`イベントは自動的に`setUserId`および`setUserProperty`イベントを送信します。
* 適切なデータが提供されている場合（**画面名**にマッピングされた変数）、`event_view_item_list`、`event_view_item`、`event_ecommerce_purchase`、および`event_begin_checkout`は自動的に`setScreenName`イベントを送信することができます。
* 単数のパラメータまたはe-commerceの配列のみを使用し、両方を使用しないでください。

## Firebaseについての注意

FirebaseはGoogle Analyticsとは異なり、用語も構成も全く異なります。変数/マッピングは一対一で変換されないため、Firebaseではカスタムディメンションが含まれていません。パラメータはカスタムディメンションの代わりに使用されるべきです。カスタムパラメータが必要な場合、Firebase内で構成することができます。

A/BテストのパラメータはFirebaseに保存されており、Tealiumにはアクセスできません。A/BテストデータをTealium内で使用する必要がある場合、データはBigQueryを使用してFirebaseから無料でエクスポートできます。その後、データをTealiumのサーバーサイド製品にインポートして、コネクターやオーディエンスで使用することができます。

## リソース

[Tealium Firebase Remote Command Integration](https://docs.tealium.com/platforms/remote-commands/integrations/firebase/)&lt;br&gt;
[Firebase Remote Command Example – iOS (Github)](https://github.com/Tealium/tealium-ios-firebase-remote-command)&lt;br&gt;
[Firebase Remote Command Example – Android (Github)](https://github.com/Tealium/tealium-android-firebase-remote-command)&lt;br&gt;
[Google Firebase Guide](https://firebase.google.com/docs/guides)&lt;br&gt;
[Automatically Collected Events – Firebase](https://support.google.com/firebase/answer/6317485?hl=en)