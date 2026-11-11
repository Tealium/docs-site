---
title: Kochavaタグ構成ガイド
description: この記事では、タグ管理アカウントでKochavaタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kochava-tag/
---
Kochavaを使用すると、ピープルベースのマーケティング担当者は、ユーザーIDの確立と拡充、オーディエンスのセグメント化とアクティベーション、および接続されているすべてのデバイスを横断したキャンペーンの測定と最適化を行うことができます。

## タグに関するヒント

* マッピングを使用して、以下を行います。
  * 標準の構成値を上書きし、カスタムパラメータを構成する。
  * 標準イベントとカスタムイベントをトリガーする。

* Autopage — ページが読み込まれるたびにページイベントを自動送信するには、`true`に構成します。page関数を手動で呼び出した場合にのみページ読み込みを送信するには、`false`に構成します。
* Cache — ブラウザによるSDKコードのキャッシュを許可するには、`true`に構成します。ページが読み込まれるたびにSDKコードを強制的に読み込むには、`false`に構成します。
* Verbose — コンソールへの詳細ログ出力を有効にするには、`true`に構成します。すべてのログ出力を抑制するには、`false`に構成します。
* Cookie Collection — サブドメインをまたいでデバイスを追跡するために、WebサイトにCookieを保存するには、`true`に構成します。Cookieを保存せず、ローカル保存のみを使用して追跡するには、`false`に構成します。

## タグの構成

新しいタグを追加するには、タグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **Kochava App GUID**
* **Autopage**
* **Cache**
* **Verbose**
* **Cookie Collection**

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリは以下のとおりです。

### 構成パラメータ

|変数|説明|
|---|---|
|アプリID| (`app_guid`)|
|アプリトラッキングの透明性が有効 (`app_tracking_transparency_enabled`)| [`true`/`false`]|
|IDリンクID| (`identity_link_ids`)|
|ログレベル| (`log_level`)|

### イベント

|変数|説明|
|---|---|
|広告のクリック| `adclick`|
|広告の表示| `adview`|
|カートに追加| `addtocart`|
|ウィッシュリストに追加| `addtowishlist`|
|実績| `achievement`|
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
|QSS（高品質ストリーミングセッション &gt; 5分）| `qss`|
|初回動画視聴| `first_video_view`|
|友人と共有| `share_with_friend`|
|認証成功| `authentication_success`|
|後で見る| `watch_later`|
|カスタム| `custom`|

### すべてのパラメータ

|変数|説明|
|---|---|
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
|アイテムの追加元| (`item_added_from`)|
|レベル| (`level`)|
|広告キャンペーンID| (`ad_campaign_id`)|
|広告キャンペーン名| (`ad_campaign_name`)|
|広告グループID| (`ad_group_id`)|
|広告グループ名| (`ad_group_name`)|
|広告メディエーション名| (`ad_mediation_name`)|
|広告ネットワーク名| (`ad_network_name`)|
|プレースメント| (`placement`)|
|広告サイズ| (`ad_size`)|
|広告タイプ| (`ad_type`)|
|最大評価値| (`max_rating_value`)|
|名前| (`name`)|
|注文ID| (`order_id`)|
|発生元| (`origin`)|
|価格| (`price`)|
|数量| (`quantity`)|
|評価値| (`rating_value`)|
|レシートID| (`receipt_id`)|
|参照元| (`referral_from`)|
|登録方法| (`registration_method`)|
|結果| (`results`)|
|スコア| (`score`)|
|検索語句| (`search_term`)|
|空間座標X| (`spatial_x`)|
|空間座標Y| (`spatial_y`)|
|空間座標Z| (`spatial_z`)|
|開始日| (`start_date`)|
|成功| (`success`)|
|ユーザーID| (`user_id`)|
|ユーザー名| (`user_name`)|
|URI| (`uri`)|
|検証済み| (`validated`)|

### イベントパラメータ

|変数|説明|
|---|---|
|広告のクリック| `adclick`|
|広告の表示| `adview`|
|カートに追加| `addtocart`|
|ウィッシュリストに追加| `addtowishlist`|
|実績| `achievement`|
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
|QSS（高品質ストリーミングセッション &gt; 5分）| `qss`|
|初回動画視聴| `first_video_view`|
|友人と共有| `share_with_friend`|
|認証成功| `authentication_success`|
|後で見る| `watch_later`|
|カスタム| `custom`|