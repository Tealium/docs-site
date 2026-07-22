---
title: Brazeモバイルリモートコマンドタグ構成ガイド
description: この記事では、Brazeモバイルリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/braze-mobile-remote-command-tag/
---
## タグのヒント

* 標準の構成値を上書きし、カスタムパラメータを構成するためにマッピングを使用します。
* これはネイティブモバイルアプリSDKのためのモバイルリモートコマンドコンパニオンタグです。

## タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスし、Brazeモバイルリモートコマンドタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加した後、以下の構成を行います：

* **APIキー**：Brazeダッシュボードから取得したアプリケーションのAPIキー
* **自動初期化**：初期化コマンドを自動的に送信します。
* **Firebase有効**
* **ADM有効**
* **自動ディープリンク開封**
* **自動位置情報収集無効**
* **ニュースフィード未読インジケータ有効**
* **Firebase送信者ID**
* **カスタムエンドポイント**
* **セッションタイムアウト（秒）**
* **通知背景色**（例：`0xFFf33e3e`）
* **トリガー間の間隔（秒）**

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### コマンド（コマンドトリガー）

以下のイベントのいずれかにトリガーをマッピングします：

|変数| 説明|
|---| ---|
|`initSDK`|  <ul><li>SDK構成</li></ul> |
|`disableSDK`|  <ul><li>データ収集無効</li></ul> |
|`changeUser`|  <ul><li>ユーザー識別</li></ul> |
|`addAlias`|  <ul><li>ユーザーエイリアス構成</li></ul> |
|`logPurchase`|  <ul><li>購入イベント</li></ul> |
|`facebookUser`|  <ul><li>Facebookユーザー</li></ul> |
|`twitterUser`|  <ul><li>Twitterユーザー</li></ul> |
|`addToSubscriptionGroup`|  <ul><li>メールまたはSMSのサブスクリプショングループにユーザーを追加</li></ul> |
|`removeFromSubscriptionGroup`|  <ul><li>メールまたはSMSのサブスクリプショングループからユーザーを削除</li></ul> |

### 位置情報

|変数| 説明|
|---| ---|
|`location_latitude`|  <ul><li>Double</li><li>緯度</li></ul> |
|`location_longitude`|  <ul><li>Double</li><li>経度</li></ul> |
|`location_latitude`|  <ul><li>Double</li><li>高度</li></ul> |
|`location_horizontal_accuracy`|  <ul><li>Double</li><li>水平精度</li></ul> |
| `location_vertical_accuracy` |  <ul><li>Double</li><li>垂直精度</li></ul> |
| `enable_automatic_geofences` | <ul><li>Boolean</li><li>Brazeジオフェンスが自動的に要求されるかどうかを構成します。デフォルト値は`true`です。</li></ul> | 

### サブスクリプション

|変数| 説明|
|---| ---|
|`email_notification`|  <ul><li>メールサブスクリプション</li><li>メールサブスクリプションタイプ構成</li><li>現在のユーザーのメールサブスクリプションの通知タイプを構成します。</li></ul> |
|`push_notification`|  <ul><li>プッシュサブスクリプション</li><li>プッシュサブスクリプションタイプ構成</li><li>現在のユーザーのプッシュ通知の通知タイプを構成します。</li></ul> |
|`subscription_group_id`|  <ul><li>サブスクリプショングループの一意の識別子。</li></ul> |

### ソーシャルデータトラッキング

|変数| 説明|
|---| ---|
|`twitterFollowingCount`|  <ul><li>Integer</li><li>Twitterフォロー数</li></ul> |
|`twitterProfileImageUrl`|  <ul><li>Twitterプロファイル画像URL</li></ul> |

### ユーザー属性

|変数| 説明|
|---| ---|
|`user_id`|  <ul><li>ユーザーID</li></ul> |
| `alias_name` |  <ul><li>エイリアス名</li><li>現在のユーザーの識別子です。</li></ul> |
| `alias_label` |  <ul><li>ユーザーエイリアスラベル</li><li>エイリアスのソースなど、エイリアスのラベルです。</li></ul> |
| `first_name` |  <ul><li>名</li></ul> |
| `last_name` |  <ul><li>姓</li></ul> |
|`gender`|  <ul><li>性別</li></ul> |
|`language`|  <ul><li>言語</li><li>表示言語のISO 639-1言語コード。</li></ul> |
|`email`|  <ul><li>メール</li></ul> |
|`home_city`|  <ul><li>居住都市</li></ul> |
|`country`|  <ul><li>国</li></ul> |
| `date_of_birth` |  <ul><li>生年月日</li></ul> |
| `phone` | <ul><li>String</li><li>ユーザーの電話番号。null値はこのユーザーの電話番号を解除します。</li></ul> |
|`unset_custom_attribute`|  <ul><li>Array</li><li>カスタム属性の解除</li></ul> |

### Eコマース

|変数| 説明|
|---| ---|
|`order_currency`|  <ul><li>通貨</li><li>`_ccurrency`を上書きします。</li></ul> |
|`product_id`|  <ul><li>Array</li><li>製品IDリスト</li><li>`_cprod`を上書きします。</li></ul> |
|`product_qty`|  <ul><li>Array</li><li>数量リスト</li><li>`_cquan`を上書きします。</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>価格リスト</li><li>`_cprice`を上書きします。</li></ul> |
| `purchase_properties.foo` |  <ul><li>カスタム購入プロパティ</li></ul> |

### 初期化

|変数| 説明|
|---| ---|
|`api_key`|  <ul><li>APIキー</li></ul> |
| `sdk_authentication_signature` | <ul><li>String</li><li>SDK認証署名</li></ul> |
| `ad_tracking_enabled` | <ul><li>Boolean</li><li>Google広告IDの広告追跡制限フィールド。Google広告IDで「広告追跡を制限」が有効になっている場合、広告追跡を無効にする必要があります。</li></ul> |
| `is_sdk_authentication_enabled` | <ul><li>Boolean</li><li>デフォルト値は`true`です。</li></ul> |
|`firebase_enabled`|  <ul><li>Boolean</li><li>Firebaseが有効です</li></ul> |
|`adm_enabled`|  <ul><li>Boolean</li><li>ADMが有効です</li></ul> |
|`auto_push_deep_links`|  <ul><li>Boolean</li><li>自動プッシュディープリンク</li></ul> |
|`enable_automatic_location`|  <ul><li>Boolean</li><li>位置情報無効</li></ul> |
|`firebase_sender_id`|  <ul><li>String</li><li>Firebase送信者ID</li></ul> |
| `small_notification_icon` |  <ul><li>String</li><li>小さい通知アイコン</li></ul> |
|`large_notification_icon`|  <ul><li>String</li><li>大きい通知アイコン</li></ul> |
|`custom_endpoint`|  <ul><li>String</li><li>カスタムエンドポイント</li></ul> |
|`session_timeout`|  <ul><li>Integer</li><li>セッションタイムアウト</li></ul> |
| `default_notification_color` |  <ul><li>Integer</li><li>デフォルトの通知色</li></ul> |
|`bad_network_interval`|  <ul><li>Integer</li><li>悪いネットワーク間隔</li></ul> |
| `good_network_interval` |  <ul><li>Integer</li><li>良いネットワーク間隔</li></ul> |
|`great_network_interval`|  <ul><li>Integer</li><li>優れたネットワーク間隔</li></ul> |
|`trigger_interval_seconds`|  <ul><li>Integer</li><li>トリガー間隔秒</li></ul> |
|`push_token`|  <ul><li>String</li><li>プッシュトークン</li></ul> |
|`enable_geofences`|  <ul><li>Boolean</li><li>ジオフェンスを有効にする</li></ul> |
| `request_processing_policy` |  <ul><li>Integer</li><li>リクエスト処理ポリシー</li></ul> |
|`flush_interval`|  <ul><li>Double</li><li>フラッシュ間隔</li></ul> |
|`device_options`|  <ul><li>Integer</li><li>デバイスオプション</li></ul> |
|`push_story_identifier`|  <ul><li>String</li><li>プッシュストーリー識別子</li></ul> |
| `backstack_activity_enabled` |  <ul><li>Boolean</li><li>バックスタックアクティビティ有効</li></ul> |
|`backstack_activity_class`|  <ul><li>String</li><li>バックスタックアクティビティクラス</li></ul> |