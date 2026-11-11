---
title: Braze Mobile Remote Commandタグ構成ガイド
description: この記事では、Braze Mobile Remote Commandタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/braze-mobile-remote-command-tag/
---
## タグに関するヒント

* マッピングを使用して標準の構成値を上書きし、カスタムパラメータを構成します。
* これは、ネイティブモバイルアプリSDK用のMobile Remote Commandコンパニオンタグです。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、以下の構成を行います。

* **APIキー**：Braze DashboardにあるアプリケーションのAPIキー
* **自動初期化**：Initializeコマンドを自動的に送信します。
* **Firebaseを有効化**
* **ADMを有効化**
* **ディープリンクを自動的に開く**
* **位置情報の自動収集を無効化**
* **ニュースフィードの未読インジケーターを有効化**
* **Firebase Sender ID**
* **カスタムエンドポイント**
* **セッションタイムアウト（秒）**
* **通知の背景色**（例：`0xFFf33e3e`）
* **トリガー間の間隔（秒）**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### コマンド（コマンドトリガー）

トリガーを、以下の1つ以上のイベントにマッピングします。

|変数|説明|
|---|---|
|`initSDK`| <ul><li>SDKのセットアップ</li></ul> |
|`disableSDK`| <ul><li>データ収集を無効化</li></ul> |
|`changeUser`| <ul><li>ユーザーを識別</li></ul> |
|`addAlias`| <ul><li>ユーザーエイリアスを構成</li></ul> |
|`logPurchase`| <ul><li>購入イベント</li></ul> |
|`facebookUser`| <ul><li>Facebookユーザー</li></ul> |
|`twitterUser`| <ul><li>Xユーザー</li></ul> |
|`addToSubscriptionGroup`| <ul><li>ユーザーをメールまたはSMSの購読グループに追加</li></ul> |
|`removeFromSubscriptionGroup`| <ul><li>ユーザーをメールまたはSMSの購読グループから削除</li></ul> |

### 位置情報

|変数|説明|
|---|---|
|`location_latitude`| <ul><li>倍精度浮動小数点数</li><li>緯度</li></ul> |
|`location_longitude`| <ul><li>倍精度浮動小数点数</li><li>経度</li></ul> |
|`location_latitude`| <ul><li>倍精度浮動小数点数</li><li>高度</li></ul> |
|`location_horizontal_accuracy`| <ul><li>倍精度浮動小数点数</li><li>水平方向の精度</li></ul> |
| `location_vertical_accuracy` | <ul><li>倍精度浮動小数点数</li><li>垂直方向の精度</li></ul> |
| `enable_automatic_geofences` | <ul><li>ブール値</li><li>Braze SDKがBraze Geofenceを自動的にリクエストするかどうかを構成します。デフォルト値は`true`です。</li></ul> |

### 購読

|変数|説明|
|---|---|
|`email_notification`| <ul><li>メール購読</li><li>メール購読タイプを構成</li><li>現在のユーザーに対するメール購読の通知タイプを構成します。</li></ul> |
|`push_notification`| <ul><li>プッシュ購読</li><li>プッシュ購読タイプを構成</li><li>現在のユーザーに対するプッシュ通知の通知タイプを構成します。</li></ul> |
|`subscription_group_id`| <ul><li>購読グループの一意の識別子。</li></ul> |

### ソーシャルデータのトラッキング

|変数|説明|
|---|---|
|`twitterFollowingCount`| <ul><li>整数</li><li>Xのフォロー数</li></ul> |
|`twitterProfileImageUrl`| <ul><li>Xのプロフィール画像URL</li></ul> |

### ユーザー属性

|変数|説明|
|---|---|
|`user_id`| <ul><li>ユーザーID</li></ul> |
| `alias_name` | <ul><li>エイリアス名</li><li>現在のユーザーの識別子。</li></ul> |
| `alias_label` | <ul><li>ユーザーエイリアスのラベル</li><li>エイリアスのソースなど、エイリアスに付けるラベル。</li></ul> |
| `first_name` | <ul><li>名</li></ul> |
| `last_name` | <ul><li>姓</li></ul> |
|`gender`| <ul><li>性別</li></ul> |
|`language`| <ul><li>言語</li><li>表示言語のISO 639-1言語コード。</li></ul> |
|`email`| <ul><li>メールアドレス</li></ul> |
|`home_city`| <ul><li>居住都市</li></ul> |
|`country`| <ul><li>国</li></ul> |
| `date_of_birth` | <ul><li>生年月日</li></ul> |
| `phone` | <ul><li>文字列</li><li>ユーザーの電話番号。null値を指定すると、このユーザーの電話番号の構成が解除されます。</li></ul> |
|`unset_custom_attribute`| <ul><li>配列</li><li>カスタム属性の構成を解除</li></ul> |

### Eコマース

|変数|説明|
|---|---|
|`order_currency`| <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul> |
|`product_id`| <ul><li>配列</li><li>商品IDのリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_qty`| <ul><li>配列</li><li>数量のリスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`| <ul><li>配列</li><li>価格のリスト</li><li>`_cprice`を上書きします。</li></ul> |
| `purchase_properties.foo` | <ul><li>カスタム購入プロパティ</li></ul> |

### 初期化

|変数|説明|
|---|---|
|`api_key`| <ul><li>APIキー</li></ul> |
| `sdk_authentication_signature` | <ul><li>文字列</li><li>SDK認証署名</li></ul> |
| `ad_tracking_enabled` | <ul><li>ブール値</li><li>Google Advertising IDの広告トラッキング制限フィールド。Google Advertising IDで「広告トラッキングを制限」が有効になっている場合、広告トラッキングを無効にする必要があることを意味します。</li></ul> |
| `is_sdk_authentication_enabled` | <ul><li>ブール値</li><li>デフォルト値は`true`です。</li></ul> |
|`firebase_enabled`| <ul><li>ブール値</li><li>Firebaseが有効</li></ul> |
|`adm_enabled`| <ul><li>ブール値</li><li>ADMが有効</li></ul> |
|`auto_push_deep_links`| <ul><li>ブール値</li><li>プッシュディープリンクを自動的に開く</li></ul> |
|`enable_automatic_location`| <ul><li>ブール値</li><li>位置情報を無効化</li></ul> |
|`firebase_sender_id`| <ul><li>文字列</li><li>Firebase Sender ID</li></ul> |
| `small_notification_icon` | <ul><li>文字列</li><li>小さい通知アイコン</li></ul> |
|`large_notification_icon`| <ul><li>文字列</li><li>大きい通知アイコン</li></ul> |
|`custom_endpoint`| <ul><li>文字列</li><li>カスタムエンドポイント</li></ul> |
|`session_timeout`| <ul><li>整数</li><li>セッションタイムアウト</li></ul> |
| `default_notification_color` | <ul><li>整数</li><li>デフォルトの通知色</li></ul> |
|`bad_network_interval`| <ul><li>整数</li><li>低品質ネットワークでの間隔</li></ul> |
| `good_network_interval` | <ul><li>整数</li><li>良好なネットワークでの間隔</li></ul> |
|`great_network_interval`| <ul><li>整数</li><li>高品質ネットワークでの間隔</li></ul> |
|`trigger_interval_seconds`| <ul><li>整数</li><li>トリガー間隔（秒）</li></ul> |
|`push_token`| <ul><li>文字列</li><li>プッシュトークン</li></ul> |
|`enable_geofences`| <ul><li>ブール値</li><li>Geofenceを有効化</li></ul> |
| `request_processing_policy` | <ul><li>整数</li><li>リクエスト処理ポリシー</li></ul> |
|`flush_interval`| <ul><li>倍精度浮動小数点数</li><li>フラッシュ間隔</li></ul> |
|`device_options`| <ul><li>整数</li><li>デバイスオプション</li></ul> |
|`push_story_identifier`| <ul><li>文字列</li><li>プッシュストーリー識別子</li></ul> |
| `backstack_activity_enabled` | <ul><li>ブール値</li><li>バックスタックアクティビティが有効</li></ul> |
|`backstack_activity_class`| <ul><li>文字列</li><li>バックスタックアクティビティクラス</li></ul> |