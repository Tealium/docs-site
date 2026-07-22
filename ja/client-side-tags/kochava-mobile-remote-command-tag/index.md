---
title: Kochavaモバイルリモートコマンドタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでKochavaモバイルリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kochava-mobile-remote-command-tag/
---
## タグのヒント

* マッピングを使用して:
  * 標準の構成値を上書きし、カスタムパラメータを構成する
  * 標準およびカスタムイベントをトリガーする

* これはネイティブモバイルアプリSDKのためのモバイルリモートコマンドコンパニオンタグです。

## タグの構成

まず、タグマーケットプレイスにアクセスしてKochavaモバイルリモートコマンドタグを追加します（タグの追加方法については[こちら](https://docs.tealium.com/manage-tags/)を参照してください）。

タグを追加した後、以下の構成を構成します：

* **アプリID**
* **アプリトラッキング透明性有効**

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 構成パラメータ

|変数| 説明|
|---| ---|
|`app_guid`|  <ul><li>アプリID</li></ul> |
|`app_tracking_transparency_enabled`|  <ul><li>アプリトラッキング透明性有効</li><li>値は `true` または `false`。</li></ul> |
|`identity_link_ids`|  <ul><li>アイデンティティリンクID</li></ul> |
|`log_level`|  <ul><li>ログレベル</li></ul> |

### イベント

|変数| 説明|
|---| ---|
|`adclick`| 広告クリック|
|`adview`| 広告表示|
|`addtocart`| カートに追加|
|`addtowishlist`| ほしい物リストに追加|
|`achievement`| 実績|
|`checkoutstart`| チェックアウト開始|
|`tutorialcomplete`| チュートリアル完了|
|`consentgranted`| 同意が与えられた|
|`initialize`| 初期化|
|`invalidate`| 無効化|
|`levelcomplete`| レベル完了|
|`purchase`| 購入|
|`pushopened`| プッシュ開封|
|`pushreceived`| プッシュ受信|
|`rating`| 評価|
|`registrationcomplete`| 登録完了|
|`search`| 検索|
|`sendidentitylink`| アイデンティティリンク送信|
|`sleeptracker`| 睡眠トラッカー|
|`setsleep`| 睡眠構成|
|`starttrial`| トライアル開始|
|`subscribe`| 登録|
|`view`| 表示|
|`custom`| カスタム|

### 全パラメータ

|変数| 説明|
|---| ---|
|`action`| アクション|
|`ad_campaign_id`| 広告キャンペーンID|
|`ad_campaign_name`| 広告キャンペーン名|
|`ad_device_type`| 広告デバイスタイプ|
|`ad_group_id`| 広告グループID|
|`ad_group_name`| 広告グループ名|
|`ad_mediation_name`| 広告仲介名|
|`ad_network_name`| 広告ネットワーク名|
|`ad_size`| 広告サイズ|
|`ad_type`| 広告タイプ|
|`app_store_receipt_encoded`| アプリストアレシートエンコード|
|`apple_watch_id`| アップルウォッチID|
|`background`| 背景|
|`checkout_as_guest`| ゲストとしてチェックアウト|
|`completed`| 完了|
|`content_id`| コンテンツID|
|`content_type`| コンテンツタイプ|
|`currency`| 通貨|
|`custom_event_name`| カスタムイベント名|
|`date_now`| 日付|
|`description`| 説明|
|`destination`| 宛先|
|`duration`| 期間|
|`end_date`| 終了日|
|`from_apple_watch`| アップルウォッチから|
|`item_added_from`| 追加元|
|`level`| レベル|
|`max_rating_value`| 最大評価値|
|`name`| 名前|
|`order_id`| 注文ID|
|`origin`| 起源|
|`placement`| 配置|
|`price`| 価格|
|`quantity`| 数量|
|`rating_value`| 評価値|
|`receipt_id`| レシートID|
|`referral_from`| 紹介元|
|`registration_method`| 登録方法|
|`results`| 結果|
|`score`| スコア|
|`search_term`| 検索語|
|`sleep`| 睡眠|
|`spatial_x`| 空間X|
|`spatial_y`| 空間Y|
|`spatial_z`| 空間Z|
|`start_date`| 開始日|
|`success`| 成功|
|`user_id`| ユーザーID|
|`user_name`| ユーザー名|
|`uri`| URI|
|`validated`| 検証済み|
|`custom`| カスタム|

### イベントパラメータ

|変数| 説明|
|---| ---|
|`adclick`| 広告クリック|
|`adview`| 広告表示|
|`addtocart`| カートに追加|
|`addtowishlist`| ほしい物リストに追加|
|`achievement`| 実績|
|`checkoutstart`| チェックアウト開始|
|`completetutorial`| チュートリアル完了|
|`consentgranted`| 同意が与えられた|
|`initialize`| 初期化|
|`invalidate`| 無効化|
|`levelcomplete`| レベル完了|
|`purchase`| 購入|
|`pushopened`| プッシュ開封|
|`pushreceived`| プッシュ受信|
|`rating`| 評価|
|`registrationcomplete`| 登録完了|
|`search`| 検索|
|`sendidentitylink`| アイデンティティリンク送信|
|`setsleep`| 睡眠構成|
|`sleeptracker`| 睡眠トラッカー|
|`starttrial`| トライアル開始|
|`subscribe`| 登録|
|`view`| 表示|
|`custom`| カスタム|