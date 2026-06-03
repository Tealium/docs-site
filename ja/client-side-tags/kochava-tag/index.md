---
title: Kochavaタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでKochavaタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kochava-tag/
---
Kochavaは、人物ベースのマーケターがユーザーのアイデンティティを確立および豊かにし、オーディエンスをセグメント化してアクティブ化し、すべての接続されたデバイスでキャンペーンを測定および最適化することを可能にします。

## タグのヒント

* マッピングを使用して：
  * 標準の構成値を上書きし、カスタムパラメータを構成します。
  * 標準およびカスタムイベントをトリガーします。

* Autopage — `true`に構成すると、ページの読み込みごとに自動的にページイベントが送信されます。`false`に構成すると、ページ関数への手動呼び出し時にのみページ読み込みが送信されます。
* Cache — `true`に構成すると、ブラウザがSDKコードをキャッシュすることを許可します。`false`に構成すると、ページの読み込みごとにSDKコードがロードされるように強制します。
* Verbose — `true`に構成すると、コンソールに詳細なログが出力されます。`false`に構成すると、すべてのログが抑制されます。
* Cookie Collection — `true`に構成すると、サブドメイン間でデバイスを追跡するためにウェブサイトにCookieを設置します。`false`に構成すると、Cookieを設置せず、追跡にはローカル保存のみを依存します。

## タグの構成

まず、タグマーケットプレイスにアクセスしてKochavaタグを追加します（[タグの追加方法についてはこちら]()を参照）。

タグを追加した後、以下の構成を構成します：

* **KochavaアプリGUID**
* **Autopage**
* **Cache**
* **Verbose**
* **Cookie Collection**

## データマッピング

マッピングは、[データレイヤー変数]()からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグ宛先にマッピングする方法については、[データマッピング](/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 構成パラメータ

|変数| 説明|
|---| ---|
|アプリID| (`app_guid`)|
|アプリ追跡透明性有効 (`app_tracking_transparency_enabled`)| [`true`/`false`]|
|アイデンティティリンクID| (`identity_link_ids`)|
|ログレベル| (`log_level`)|

### イベント

|変数| 説明|
|---| ---|
|広告クリック| `adclick`|
|広告表示| `adview`|
|カートに追加| `addtocart`|
|ウィッシュリストに追加| `addtowishlist`|
|成果| `achievement`|
|チェックアウト開始| `checkoutstart`|
|チュートリアル完了| `tutorialcomplete`|
|レベル完了| `levelcomplete`|
|購入| `purchase`|
|評価| `rating`|
|登録完了| `registrationcomplete`|
|検索| `search`|
|トライアル開始| `starttrial`|
|購読| `subscribe`|
|表示| `view`|
|QSS. (品質ストリーミングセッション&amp;gt;5分)| `qss`|
|初ビデオ視聴| `first_video_view`|
|友人と共有| `share_with_friend`|
|認証成功| `authentication_success`|
|後で見る| `watch_later`|
|カスタム| `custom`|

### すべてのパラメータ

|変数| 説明|
|---| ---|
|アクション| (`action`)|
|バックグラウンド| (`background`)|
|ゲストとしてチェックアウト| (`checkout_as_guest`)|
|完了| (`completed`)|
|コンテンツID| (`content_id`)|
|コンテンツタイプ| (`content_type`)|
|通貨| (`currency`)|
|日付| (`now_date`)|
|説明| (`description`)|
|目的地| (`destination`)|
|期間| (`duration`)|
|終了日| (`end_date`)|
|アイテム追加元| (`item_added_from`)|
|レベル| (`level`)|
|広告キャンペーンID| (`ad_campaign_id`)|
|広告キャンペーン名| (`ad_campaign_name`)|
|広告グループID| (`ad_group_id`)|
|広告グループ名| (`ad_group_name`)|
|広告仲介名| (`ad_mediation_name`)|
|広告ネットワーク名| (`ad_network_name`)|
|配置| (`placement`)|
|広告サイズ| (`ad_size`)|
|広告タイプ| (`ad_type`)|
|最大評価値| (`max_rating_value`)|
|名前| (`name`)|
|注文ID| (`order_id`)|
|起源| (`origin`)|
|価格| (`price`)|
|数量| (`quantity`)|
|評価値| (`rating_value`)|
|領収書ID| (`receipt_id`)|
|紹介元| (`referral_from`)|
|登録方法| (`registration_method`)|
|結果| (`results`)|
|スコア| (`score`)|
|検索語| (`search_term`)|
|空間X| (`spatial_x`)|
|空間Y| (`spatial_y`)|
|空間Z| (`spatial_z`)|
|開始日| (`start_date`)|
|成功| (`success`)|
|ユーザーID| (`user_id`)|
|ユーザー名| (`user_name`)|
|URI| (`uri`)|
|検証済み| (`validated`)|

### イベントパラメータ

|変数| 説明|
|---| ---|
|広告クリック| `adclick`|
|広告表示| `adview`|
|カートに追加| `addtocart`|
|ウィッシュリストに追加| `addtowishlist`|
|成果| `achievement`|
|チェックアウト開始| `checkoutstart`|
|チュートリアル完了| `tutorialcomplete`|
|レベル完了| `levelcomplete`|
|購入| `purchase`|
|評価| `rating`|
|登録完了| `registrationcomplete`|
|検索| `search`|
|トライアル開始| `starttrial`|
|購読| `subscribe`|
|表示| `view`|
|QSS. (品質ストリーミングセッション&amp;gt;5分)| `qss`|
|初ビデオ視聴| `first_video_view`|
|友人と共有| `share_with_friend`|
|認証成功| `authentication_success`|
|後で見る| `watch_later`|
|カスタム| `custom`|