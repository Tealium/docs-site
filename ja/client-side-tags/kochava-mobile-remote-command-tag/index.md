---
title: Kochava Mobileリモートコマンドタグ構成ガイド
description: この記事では、タグ管理アカウントでKochava Mobileリモートコマンドタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kochava-mobile-remote-command-tag/
---
## タグに関するヒント

* マッピングを使用すると、次のことができます。
  * 標準の構成値を上書きし、カスタムパラメータを構成する
  * 標準イベントとカスタムイベントをトリガーする

* これは、ネイティブモバイルアプリSDK用のMobileリモートコマンドコンパニオンタグです。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **アプリID**
* **アプリトラッキングの透明性の有効化**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 構成パラメータ

|変数|説明|
|---|---|
|`app_guid`| <ul><li>アプリID</li></ul> |
|`app_tracking_transparency_enabled`| <ul><li>アプリトラッキングの透明性の有効化</li><li>値は`true`または`false`です。</li></ul> |
|`identity_link_ids`| <ul><li>Identity Link ID</li></ul> |
|`log_level`| <ul><li>ログレベル</li></ul> |

### イベント

|変数|説明|
|---|---|
|`adclick`| 広告クリック|
|`adview`| 広告表示|
|`addtocart`| カートに追加|
|`addtowishlist`| 欲しいものリストに追加|
|`achievement`| 実績|
|`checkoutstart`| チェックアウト開始|
|`tutorialcomplete`| チュートリアル完了|
|`consentgranted`| 同意取得|
|`initialize`| 初期化|
|`invalidate`| 無効化|
|`levelcomplete`| レベル完了|
|`purchase`| 購入|
|`pushopened`| プッシュ通知を開く|
|`pushreceived`| プッシュ通知を受信|
|`rating`| 評価|
|`registrationcomplete`| 登録完了|
|`search`| 検索|
|`sendidentitylink`| Identity Linkを送信|
|`sleeptracker`| 睡眠トラッカー|
|`setsleep`| 睡眠を構成|
|`starttrial`| トライアル開始|
|`subscribe`| 購読|
|`view`| 表示|
|`custom`| カスタム|

### すべてのパラメータ

|変数|説明|
|---|---|
|`action`| アクション|
|`ad_campaign_id`| 広告キャンペーンID|
|`ad_campaign_name`| 広告キャンペーン名|
|`ad_device_type`| 広告デバイスタイプ|
|`ad_group_id`| 広告グループID|
|`ad_group_name`| 広告グループ名|
|`ad_mediation_name`| 広告メディエーション名|
|`ad_network_name`| 広告ネットワーク名|
|`ad_size`| 広告サイズ|
|`ad_type`| 広告タイプ|
|`app_store_receipt_encoded`| エンコード済みApp Storeレシート|
|`apple_watch_id`| Apple Watch ID|
|`background`| バックグラウンド|
|`checkout_as_guest`| ゲストとしてチェックアウト|
|`completed`| 完了|
|`content_id`| コンテンツID|
|`content_type`| コンテンツタイプ|
|`currency`| 通貨|
|`custom_event_name`| カスタムイベント名|
|`date_now`| 日付|
|`description`| 説明|
|`destination`| 移動先|
|`duration`| 期間|
|`end_date`| 終了日|
|`from_apple_watch`| Apple Watchから|
|`item_added_from`| アイテムの追加元|
|`level`| レベル|
|`max_rating_value`| 最大評価値|
|`name`| 名前|
|`order_id`| 注文ID|
|`origin`| 起点|
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
|`spatial_x`| 空間座標X|
|`spatial_y`| 空間座標Y|
|`spatial_z`| 空間座標Z|
|`start_date`| 開始日|
|`success`| 成功|
|`user_id`| ユーザーID|
|`user_name`| ユーザー名|
|`uri`| URI|
|`validated`| 検証済み|
|`custom`| カスタム|

### イベントパラメータ

|変数|説明|
|---|---|
|`adclick`| 広告クリック|
|`adview`| 広告表示|
|`addtocart`| カートに追加|
|`addtowishlist`| 欲しいものリストに追加|
|`achievement`| 実績|
|`checkoutstart`| チェックアウト開始|
|`completetutorial`| チュートリアルを完了|
|`consentgranted`| 同意取得|
|`initialize`| 初期化|
|`invalidate`| 無効化|
|`levelcomplete`| レベル完了|
|`purchase`| 購入|
|`pushopened`| プッシュ通知を開く|
|`pushreceived`| プッシュ通知を受信|
|`rating`| 評価|
|`registrationcomplete`| 登録完了|
|`search`| 検索|
|`sendidentitylink`| Identity Linkを送信|
|`setsleep`| 睡眠を構成|
|`sleeptracker`| 睡眠トラッカー|
|`starttrial`| トライアル開始|
|`subscribe`| 購読|
|`view`| 表示|
|`custom`| カスタム|