---
title: Brazeモバイルリモートコマンドタグ構成ガイド
description: この記事では、Brazeモバイルリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/braze-mobile-remote-command-tag/
---
## タグのヒント

* 標準の構成値を上書きし、カスタムパラメータを構成するためにマッピングを使用します。
* これはネイティブモバイルアプリSDKのためのモバイルリモートコマンドコンパニオンタグです。

## タグの構成

まず、Tealiumのタグマーケットプレイスにアクセスし、Brazeモバイルリモートコマンドタグを追加します（[タグの追加方法]()について詳しくはこちら）。

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

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### コマンド（コマンドトリガー）

以下のイベントのいずれかにトリガーをマッピングします：

|変数| 説明|
|---| ---|
|`initSDK`|  &lt;ul&gt;&lt;li&gt;SDK構成&lt;/li&gt;&lt;/ul&gt; |
|`disableSDK`|  &lt;ul&gt;&lt;li&gt;データ収集無効&lt;/li&gt;&lt;/ul&gt; |
|`changeUser`|  &lt;ul&gt;&lt;li&gt;ユーザー識別&lt;/li&gt;&lt;/ul&gt; |
|`addAlias`|  &lt;ul&gt;&lt;li&gt;ユーザーエイリアス構成&lt;/li&gt;&lt;/ul&gt; |
|`logPurchase`|  &lt;ul&gt;&lt;li&gt;購入イベント&lt;/li&gt;&lt;/ul&gt; |
|`facebookUser`|  &lt;ul&gt;&lt;li&gt;Facebookユーザー&lt;/li&gt;&lt;/ul&gt; |
|`twitterUser`|  &lt;ul&gt;&lt;li&gt;Twitterユーザー&lt;/li&gt;&lt;/ul&gt; |
|`addToSubscriptionGroup`|  &lt;ul&gt;&lt;li&gt;メールまたはSMSのサブスクリプショングループにユーザーを追加&lt;/li&gt;&lt;/ul&gt; |
|`removeFromSubscriptionGroup`|  &lt;ul&gt;&lt;li&gt;メールまたはSMSのサブスクリプショングループからユーザーを削除&lt;/li&gt;&lt;/ul&gt; |

### 位置情報

|変数| 説明|
|---| ---|
|`location_latitude`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;緯度&lt;/li&gt;&lt;/ul&gt; |
|`location_longitude`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;経度&lt;/li&gt;&lt;/ul&gt; |
|`location_latitude`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;高度&lt;/li&gt;&lt;/ul&gt; |
|`location_horizontal_accuracy`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;水平精度&lt;/li&gt;&lt;/ul&gt; |
| `location_vertical_accuracy` |  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;垂直精度&lt;/li&gt;&lt;/ul&gt; |
| `enable_automatic_geofences` | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Brazeジオフェンスが自動的に要求されるかどうかを構成します。デフォルト値は`true`です。&lt;/li&gt;&lt;/ul&gt; | 

### サブスクリプション

|変数| 説明|
|---| ---|
|`email_notification`|  &lt;ul&gt;&lt;li&gt;メールサブスクリプション&lt;/li&gt;&lt;li&gt;メールサブスクリプションタイプ構成&lt;/li&gt;&lt;li&gt;現在のユーザーのメールサブスクリプションの通知タイプを構成します。&lt;/li&gt;&lt;/ul&gt; |
|`push_notification`|  &lt;ul&gt;&lt;li&gt;プッシュサブスクリプション&lt;/li&gt;&lt;li&gt;プッシュサブスクリプションタイプ構成&lt;/li&gt;&lt;li&gt;現在のユーザーのプッシュ通知の通知タイプを構成します。&lt;/li&gt;&lt;/ul&gt; |
|`subscription_group_id`|  &lt;ul&gt;&lt;li&gt;サブスクリプショングループの一意の識別子。&lt;/li&gt;&lt;/ul&gt; |

### ソーシャルデータトラッキング

|変数| 説明|
|---| ---|
|`twitterFollowingCount`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;Twitterフォロー数&lt;/li&gt;&lt;/ul&gt; |
|`twitterProfileImageUrl`|  &lt;ul&gt;&lt;li&gt;Twitterプロファイル画像URL&lt;/li&gt;&lt;/ul&gt; |

### ユーザー属性

|変数| 説明|
|---| ---|
|`user_id`|  &lt;ul&gt;&lt;li&gt;ユーザーID&lt;/li&gt;&lt;/ul&gt; |
| `alias_name` |  &lt;ul&gt;&lt;li&gt;エイリアス名&lt;/li&gt;&lt;li&gt;現在のユーザーの識別子です。&lt;/li&gt;&lt;/ul&gt; |
| `alias_label` |  &lt;ul&gt;&lt;li&gt;ユーザーエイリアスラベル&lt;/li&gt;&lt;li&gt;エイリアスのソースなど、エイリアスのラベルです。&lt;/li&gt;&lt;/ul&gt; |
| `first_name` |  &lt;ul&gt;&lt;li&gt;名&lt;/li&gt;&lt;/ul&gt; |
| `last_name` |  &lt;ul&gt;&lt;li&gt;姓&lt;/li&gt;&lt;/ul&gt; |
|`gender`|  &lt;ul&gt;&lt;li&gt;性別&lt;/li&gt;&lt;/ul&gt; |
|`language`|  &lt;ul&gt;&lt;li&gt;言語&lt;/li&gt;&lt;li&gt;表示言語のISO 639-1言語コード。&lt;/li&gt;&lt;/ul&gt; |
|`email`|  &lt;ul&gt;&lt;li&gt;メール&lt;/li&gt;&lt;/ul&gt; |
|`home_city`|  &lt;ul&gt;&lt;li&gt;居住都市&lt;/li&gt;&lt;/ul&gt; |
|`country`|  &lt;ul&gt;&lt;li&gt;国&lt;/li&gt;&lt;/ul&gt; |
| `date_of_birth` |  &lt;ul&gt;&lt;li&gt;生年月日&lt;/li&gt;&lt;/ul&gt; |
| `phone` | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;ユーザーの電話番号。null値はこのユーザーの電話番号を解除します。&lt;/li&gt;&lt;/ul&gt; |
|`unset_custom_attribute`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;カスタム属性の解除&lt;/li&gt;&lt;/ul&gt; |

### Eコマース

|変数| 説明|
|---| ---|
|`order_currency`|  &lt;ul&gt;&lt;li&gt;通貨&lt;/li&gt;&lt;li&gt;`_ccurrency`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;製品IDリスト&lt;/li&gt;&lt;li&gt;`_cprod`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_qty`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;数量リスト&lt;/li&gt;&lt;li&gt;`_cquan`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;価格リスト&lt;/li&gt;&lt;li&gt;`_cprice`を上書きします。&lt;/li&gt;&lt;/ul&gt; |
| `purchase_properties.foo` |  &lt;ul&gt;&lt;li&gt;カスタム購入プロパティ&lt;/li&gt;&lt;/ul&gt; |

### 初期化

|変数| 説明|
|---| ---|
|`api_key`|  &lt;ul&gt;&lt;li&gt;APIキー&lt;/li&gt;&lt;/ul&gt; |
| `sdk_authentication_signature` | &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;SDK認証署名&lt;/li&gt;&lt;/ul&gt; |
| `ad_tracking_enabled` | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Google広告IDの広告追跡制限フィールド。Google広告IDで「広告追跡を制限」が有効になっている場合、広告追跡を無効にする必要があります。&lt;/li&gt;&lt;/ul&gt; |
| `is_sdk_authentication_enabled` | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;デフォルト値は`true`です。&lt;/li&gt;&lt;/ul&gt; |
|`firebase_enabled`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;Firebaseが有効です&lt;/li&gt;&lt;/ul&gt; |
|`adm_enabled`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;ADMが有効です&lt;/li&gt;&lt;/ul&gt; |
|`auto_push_deep_links`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;自動プッシュディープリンク&lt;/li&gt;&lt;/ul&gt; |
|`enable_automatic_location`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;位置情報無効&lt;/li&gt;&lt;/ul&gt; |
|`firebase_sender_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Firebase送信者ID&lt;/li&gt;&lt;/ul&gt; |
| `small_notification_icon` |  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;小さい通知アイコン&lt;/li&gt;&lt;/ul&gt; |
|`large_notification_icon`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;大きい通知アイコン&lt;/li&gt;&lt;/ul&gt; |
|`custom_endpoint`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;カスタムエンドポイント&lt;/li&gt;&lt;/ul&gt; |
|`session_timeout`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;セッションタイムアウト&lt;/li&gt;&lt;/ul&gt; |
| `default_notification_color` |  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;デフォルトの通知色&lt;/li&gt;&lt;/ul&gt; |
|`bad_network_interval`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;悪いネットワーク間隔&lt;/li&gt;&lt;/ul&gt; |
| `good_network_interval` |  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;良いネットワーク間隔&lt;/li&gt;&lt;/ul&gt; |
|`great_network_interval`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;優れたネットワーク間隔&lt;/li&gt;&lt;/ul&gt; |
|`trigger_interval_seconds`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;トリガー間隔秒&lt;/li&gt;&lt;/ul&gt; |
|`push_token`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;プッシュトークン&lt;/li&gt;&lt;/ul&gt; |
|`enable_geofences`|  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;ジオフェンスを有効にする&lt;/li&gt;&lt;/ul&gt; |
| `request_processing_policy` |  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;リクエスト処理ポリシー&lt;/li&gt;&lt;/ul&gt; |
|`flush_interval`|  &lt;ul&gt;&lt;li&gt;Double&lt;/li&gt;&lt;li&gt;フラッシュ間隔&lt;/li&gt;&lt;/ul&gt; |
|`device_options`|  &lt;ul&gt;&lt;li&gt;Integer&lt;/li&gt;&lt;li&gt;デバイスオプション&lt;/li&gt;&lt;/ul&gt; |
|`push_story_identifier`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;プッシュストーリー識別子&lt;/li&gt;&lt;/ul&gt; |
| `backstack_activity_enabled` |  &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;li&gt;バックスタックアクティビティ有効&lt;/li&gt;&lt;/ul&gt; |
|`backstack_activity_class`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;バックスタックアクティビティクラス&lt;/li&gt;&lt;/ul&gt; |