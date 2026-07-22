---
title: ピアノアナリティクスタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでピアノアナリティクスタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/piano-analytics-tag/
---
## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。
* **Set Consent Mode** パラメーターは、`opt-in`、`essential`、または `opt-out` の値のみを受け付けます。

このタグは、次のベンダーSDKに基づいています: [Piano Analytics: Javascript](https://developers.atinternet-solutions.com/piano-analytics/data-collection/sdks/javascript).

## タグの構成

タグマーケットプレイスにアクセスして新しいタグを追加します。タグを追加する一般的な手順については、[Tag Overview](https://docs.tealium.com/about-tags/) の記事を読んでください。

タグを追加する際には、以下の構成を構成します:

* **Site ID**: ATインターネットのサイトID。
* **Collection Domain**: ATインターネットのデータ収集ドメイン。
* **Collection Path**: ATインターネットのピクセルリクエストURLパス。
* **Add Event URL**: すべてのイベントに現在のページのURLを含む `page_url` プロパティを自動的に追加します。デフォルト値は `withoutQS` です。
* **Require Consent**: 同意機能をアクティブにするには、`requireConsent` 変数を `true` に構成します。
* **Send Event When Opt-out**: オプトアウト時にイベントを送信しますか？デフォルト値は `true` です。
* **Campaign Prefix**: 優先順位を持ってキャンペーンのタイプを選択します。
* **Enable UTM Tracking**: UTMパラメーターをプロパティとして収集します。デフォルト値は `true` です。
* **Queue Name**: デフォルトの `queueName` を `_pac` から上書きするためにこのフィールドを使用します。
* **Privacy Default Mode**: プライバシーのデフォルトモードを選択します: `opt-in`、`essential`、または `opt-out`。
* **Automatically read from Tealium Consent Cookie**: Tealium Consent Managerと統合します。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/) のドキュメントを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。変数をタグの宛先にマッピングする方法については、[data mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/) を参照してください。

利用可能なカテゴリは以下の通りです:

### タグ構成パラメータ

| 変数                  | タイプ      | 説明             |
|:--------------------------|:----------|:------------------------|
|  `site`                   | 文字列    | サイトID。                | 
|  `collectionDomain`       | 文字列    | 収集ドメイン。      | 
|  `collectionPath`         | 文字列    | 収集パス。        | 
|  `addEventURL`            | ブール値   | イベントURLを追加。          | 
|  `sendEventWhenOptout`    | ブール値   | オプトアウト時にイベントを送信。 | 
|  `campaignPrefix`         | 文字列    | キャンペーンプレフィックス。        | 
|  `enableUTMTracking`      | ブール値   | UTMトラッキングを有効にする。    | 
| `queueName`               | 文字列    | キュー名。             | 

### 変換パラメータ

| 変数    | タイプ        | 説明 |
|:------------|:------------|:------------|
| `goal_type` | 文字列      | ゴールタイプ。  |

### ページパラメータ

| 変数        | タイプ      | 説明     |
|:----------------|:----------|:----------------|
| `page`          | 文字列    | ページ。           |
| `page_chapter1` | 文字列    | ページチャプター1。 |
| `page_chapter2` | 文字列    | ページチャプター2。 |
| `page_chapter3` | 文字列    | ページチャプター3。 |

### クリックパラメータ

| 変数         | タイプ      |説明       |
|:-----------------|:----------|:-----------------|
| `click`          | 文字列    | クリック。           |
| `click_chapter1` | 文字列    | クリックチャプター1。 |
| `click_chapter2` | 文字列    | クリックチャプター2。 |
| `click_chapter3` | 文字列    | クリックチャプター3。 |

### サイト内広告パラメータ

| 変数                       | タイプ    | 説明                    |
|:-------------------------------|:--------|:-------------------------------|
|  `onsitead_type` (必須)    | 文字列  | サイト内広告タイプ。               |
|  `onsitead_advertiser`         | 文字列  | サイト内広告の広告主。         |
|  `onsitead_campaign`           | 文字列  | サイト内広告キャンペーン。           |
|  `onsitead_category`           | 文字列  | サイト内広告カテゴリ。           |
|  `onsitead_creation`           | 文字列  | サイト内広告作成。           |
|  `onsitead_detailed_placement` | 文字列  | サイト内広告の詳細な配置。 |
|  `onsitead_format`             | 文字列  | サイト内広告フォーマット。             |
|  `onsitead_general_placement`  | 文字列  | サイト内広告の一般的な配置。  |
|  `onsitead_url`                | 文字列  | サイト内広告URL。                |
|  `onsitead_variant`            | 文字列  | サイト内広告バリアント。            |

### ISE (内部検索エンジン) パラメータ

| 変数         | タイプ    | 説明     |
|:-----------------|:--------|:----------------|
| `ise_keyword`    | 文字列  | ISEキーワード。    |
| `ise_page`       | 数値  | ISEページ。       |
| `ise_click_rank` | 数値  | ISEクリックランク。 |

### MV (多変量) テストパラメータ

| 変数      | タイプ   |説明   |
|:--------------|:-------|:-------------|
| `mv_creation` | 文字列 | 多変量作成。 |
| `mv_test`     | 文字列 | 多変量テスト。     |
| `mv_wave`     | 数値 | 多変量ウェーブ。     |

### 製品パラメータ

| 変数                                         | タイプ              | 説明                           |
|:-------------------------------------------------|:------------------|:--------------------------------------|
| `product_id` (Overrides `_cprod`)                | 文字列の配列  | 製品ID。                           |
| `product` (Overrides `_cprodname`)               | 文字列の配列  | 製品ラベル。                        |
| `product_variant`                                | 文字列            | 製品バリアント。                      |
| `product_brand` (Overrides `_cbrand`)            | 文字列の配列  | 製品ブランド。                        |
| `product_discount` (Overrides `_cpdisc`)         | ブール値の配列 | 製品が廃止されたかどうか。  |
| `product_pricetaxincluded` (Overrides `_cprice`) | 数値の配列  | 税込み価格。                  |
| `product_pricetaxfree`                           | 数値            | 税抜き価格。                      |
| `product_currency`                               | 文字列            | 通貨（ISO 4217）。                  |
| `product_stock`                                  | ブール値           | 製品が在庫ありか。      |
| `product_quantity` (Overrides `_cquan`)          | 数値の配列  | 製品数量。                     |
| `product_category1` (Overrides `_ccat`)          | 文字列の配列  | カテゴリーレベル1。                     |
| `product_category2` (Overrides `_ccat2`)         | 文字列の配列  | カテゴリーレベル2。                     |
| `product_category3`                              | 文字列            | カテゴリーレベル3。                     |
| `product_category4`                              | 文字列            | カテゴリーレベル4。                     |
| `product_cartcreation`                           | ブール値           | この製品の追加によってカートが作成されたか。 |

### カートパラメータ

| 変数                                       | 型     | 説明                                               |
|:-------------------------------------------|:-------|:---------------------------------------------------|
| `cart_id` (Overrides `_corder`)            | 文字列 | カートID。                                          |
| `cart_currency` (Overrides `_ccurrency`)   | 文字列 | カート通貨。                                        |
| `cart_turnovertaxincluded`                 | 数値   | 税込み売上。                                        |
| `cart_turnovertaxfree`                     | 数値   | 税抜き売上。                                        |
| `cart_creation_utc`                        | 数値   | カート作成日時（UTC秒）。                          |
| `cart_quantity` (Overrides `_ctotal`)      | 数値   | 商品数。                                            |
| `cart_nbdistinctproduct`                   | 数値   | 異なる商品の数。                                    |
| `cart_version`                             | 数値   | カートに関連付けられた新しい一意のバージョン識別子。 |

### トランザクションパラメータ

| 変数                          | 型               | 説明                                               |
|:------------------------------|:-----------------|:---------------------------------------------------|
| `transaction_id`              | 文字列           | トランザクションID。                               |
| `transaction_promocode`       | 文字列の配列     | プロモーションコードリスト。                       |
| `transaction_firstpurchase`   | ブール値         | 顧客にとってこれが最初の購入かどうか。             |

### 配送および支払いパラメータ

| 変数                          | 型     | 説明                       |
|:------------------------------|:-------|:---------------------------|
| `shipping_delivery`           | 文字列 | 配送タイプ。                |
| `shipping_costtaxincluded`    | 数値   | 税込み配送料。              |
| `shipping_costtaxfree`        | 数値   | 税抜き配送料。              |
| `payment_mode`                | 文字列 | 支払い方式。                |

### ユーザーパラメータ

| 変数               | 型       | 説明                                           |
|:-------------------|:---------|:-----------------------------------------------|
| `visitorId`        | 文字列   | カスタム訪問ID（GUIDまたは16文字）。         |
| `userId`           | 文字列   | ユーザーID。                                   |
| `userCategory`     | 文字列   | ユーザーカテゴリ。                              |
| `enableStorage`    | ブール値 | 保存を有効にするか。                     |

### グローバルパラメータ

| 変数                    | 型       | 説明                                                         |
|:------------------------|:---------|:-------------------------------------------------------------|
| `cookieDomain`          | 文字列   | アナリティクススクリプトによって構成されるトラッキングクッキーのドメイン範囲。 |
| `cookieSameSite`        | 文字列   | クライアント側のクッキーの**SameSite**フラグ。               |
| `cookieSecure`          | ブール値 | クライアント側のクッキーの**Secure**フラグ。                 |
| `encodeStorageBase64`   | ブール値 | クッキーがBase64エンコードされているかどうか。               |

### プライバシーおよび保存パラメータ

| 変数                       | 型       | 説明                                               |
|:---------------------------|:---------|:---------------------------------------------------|
| `privacyDefaultMode`       | 文字列   | デフォルトのプライバシーモード。                    |
| `mode`                     | 文字列   | 同意モード。                                        |
| `requireConsent`           | 文字列   | 同意が必要。                                        |
| `tealium_consent`          | ブール値 | ティーリアムの同意。                                  |
| `properties`               | オブジェクト | プロパティの優先度構成。                           |
| `consent_events`           | オブジェクト | イベントの優先度構成。                             |
| `storageLifetimePrivacy`   | 数値     | プライバシーの保存寿命値。                    |
| `storageLifetimeUser`      | 数値     | ユーザーの保存寿命値。                        |
| `storageLifetimeVisitor`   | 数値     | 訪問の保存寿命値。                          |
| `visitorStorageMode`       | 文字列   | 訪問のクッキー寿命値（相対または固定）。          |

### 訪問ポリシーパラメータ

| 変数                     | 型       | 説明 |
|:-------------------------|:---------|:-----|
| `isVisitorClientSide`    | ブール値 | 訪問IDがブラウザのクッキーに保存されているかどうか。<ul><li>`true`: 訪問IDはブラウザで生成および保存されます。</li><li>`false`: 訪問IDはサーバーで管理されます。</li></ul> |

### オーディオビデオパラメータ

| 変数                             | 型                 | 説明                                      |
|:---------------------------------|:-------------------|:------------------------------------------|
| Playback session ID              | 文字列             | 再生セッションID。                        |
| `heartbeatDuration`              | [数値またはオブジェクト] | 再生中の2つのハートビート間の遅延、最小遅延は5秒。 |
| `bufferingHeartbeatDuration`     | [数値またはオブジェクト] | バッファリング中の2つのハートビート間の遅延、最小遅延は1秒。|
| `av_session_id`                  | 文字列             | SDKによって生成されたセッションID。       |
| `av_content_id`                  | 文字列             | コンテンツID。                            |
| `av_content`                     | 文字列             | コンテンツラベル。                        |
| `av_content_type`                | 文字列             | コンテンツタイプ。                        |
| `av_content_duration`            | 数値               | コンテンツの持続時間（ミリ秒）。          |
| `av_content_linked`              | 文字列             | 関連コンテンツラベル。                    |
| `av_publication_date`            | 数値               | 公開日、タイムスタンプ。                  |
| `av_content_genre`               | 文字列の配列       | コンテンツジャンル。                      |
| `av_show`                        | 文字列             | ショーラベル。                            |
| `av_show_season`                 | 文字列             | シーズンラベル。                          |
| `av_episode_id`                  | 文字列             | エピソードID。                            |
| `av_episode`                     | 文字列             | エピソードラベル。                        |
| `av_channel`                     | 文字列             | チャンネルラベル。                        |
| `av_author`                      | 文字列             | 作者名。                                  |
| `av_content_version`             | 文字列             | コンテンツバージョン。                    |
| `av_content_duration_range`      | 文字列             | 持続時間範囲。                            |
| `av_broadcasting_type`           | 文字列             | 放送タイプ。                              |
| `av_broadcaster`                 | 文字列             | 放送者名。                                |
| `av_ad_type`                     | 文字列             | 広告タイプ。                              |
| `av_player`                      | 文字列             | プレイヤーラベル。                        |
| `av_player_version`              | 文字列             | プレイヤーバージョン。                    |
| `av_player_position`             | 文字列             | プレイヤー位置。                          |
| `av_auto_mode`                   | ブール値           | 自動再生モード。                          |
| `av_language`                    | 文字列             | メディア言語。                            |
| `av_subtitles`                   | 文字列             | 字幕。                                    |
| `av_launch_reason`               | 文字列             | 開始理由。                                |
### トラフィックソース

| 変数                     | タイプ   | 説明                   |
|:-------------------------|:--------|:----------------------|
| `src`                    | 文字列   | ソース。               |
| `src_details`            | 文字列   | ソースの詳細。         |
| `src_type`               | 文字列   | キャンペーンの自然。   |
| `src_medium`             | 文字列   | キャンペーンのタイプ。 |
| `src_campaign`           | 文字列   | キャンペーン名。       |
| `src_se_category`        | 文字列   | 検索エンジンのカテゴリ。 |
| `src_portal_site_id`     | 文字列   | ポータルサイトID。     |

### エンリッチメントされたマーケティングソース検出

| 変数                          | タイプ    | 説明                  |
|:------------------------------|:---------|:---------------------|
| `src_content`                 | 文字列    | ソースコンテンツ。    |
| `src_creative_format`         | 文字列    | クリエイティブフォーマット。 |
| `src_id`                      | 文字列    | ソースID。            |
| `src_marketing_tactic`        | 文字列    | マーケティング戦術。  |
| `src_source`                  | 文字列    | ソース。              |
| `src_source_platform`         | 文字列    | ソースプラットフォーム。 |
| `src_term`                    | 文字列    | ソースターム。        |
| `event_collection_auto`       | ブーリアン | 自動イベント収集。    |
| `geo_country_code_alpha2`     | 文字列    | 国。                  |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

| 変数                                   | 説明                                 |
|:---------------------------------------|:------------------------------------|
| `page.display`                         | ページ表示。                         |
| `click.action`                         | クリックアクション。                 |
| `click.navigation`                     | クリックナビゲーション。             |
| `click.download`                       | クリックダウンロード。               |
| `click.exit`                           | クリック終了。                       |
| `publisher.impression`                 | パブリッシャーインプレッション。     |
| `publisher.click`                      | パブリッシャークリック。             |
| `self_promotion.impression`            | セルフプロモーションインプレッション。 |
| `self_promotion.click`                 | セルフプロモーションクリック。       |
| `internal_search_result.display`       | 内部検索結果表示。                   |
| `internal_search_result.click`         | 内部検索結果クリック。               |
| `mv_test.display`                      | MVテスト表示。                       |
| `product.display`                      | 製品表示。                           |
| `product.page_display`                 | 製品ページ表示。                     |
| `product.add_to_cart`                  | カートに追加された製品。             |
| `product.remove_from_cart`             | カートから削除された製品。           |
| `product.awaiting_payment`             | 支払い待ちの製品。                   |
| `product.purchased`                    | 購入された製品。                     |
| `cart.creation`                        | カート作成。                         |
| `cart.display`                         | カート表示。                         |
| `cart.update`                          | カート更新。                         |
| `cart.delivery`                        | カート配送。                         |
| `cart.payment`                         | カート支払い。                       |
| `cart.awaiting_payment`                | 支払い待ちのカート。                 |
| `transaction.confirmation`             | 取引確認。                           |
| `setUser`                              | ユーザー構成。                       |
| `getUser`                              | ユーザー取得。                       |
| `deleteUser`                           | ユーザー削除。                       |
| `getSessionID`                         | セッションID取得。                   |
| `av.play`                              | AV再生。                             |
| `av.buffer.start`                      | AVバッファ開始。                     |
| `av.buffer.heartbeat`                  | AVバッファハートビート。             |
| `av.start`                             | AV開始。                             |
| `av.heartbeat`                         | AVハートビート。                     |
| `av.pause`                             | AV一時停止。                         |
| `av.rebuffer.start`                    | AVリバッファ開始。                   |
| `av.rebuffer.heartbeat`                | AVリバッファハートビート。           |
| `av.resume`                            | AV再開。                             |
| `av.stop`                              | AV停止。                             |
| `av.seek.start`                        | AVシーク開始。                       |
| `av.forward`                           | AV早送り。                           |
| `av.backward`                          | AV巻き戻し。                         |
| `av.ad.click`                          | AV広告クリック。                     |
| `av.ad.skip`                           | AV広告スキップ。                     |
| `av.error`                             | AVエラー。                           |
| `av.display`                           | AV表示。                             |
| `av.close`                             | AV閉じる。                           |
| `av.volume`                            | AV音量。                             |
| `av.subtitle.on`                       | AV字幕オン。                         |
| `av.subtitle.off`                      | AV字幕オフ。                         |
| `av.fullscreen.on`                     | AVフルスクリーンオン。               |
| `av.fullscreen.off`                    | AVフルスクリーンオフ。               |
| `av.quality`                           | AV品質。                             |
| `av.speed`                             | AV速度。                             |
| `av.share`                             | AV共有。                             |
| `set.mode`                             | モード構成。                         |
| `get.mode`                             | モード取得。                         |
| `disableconsent`                       | 同意無効。`mode`を`opt-out`に構成。 |
| カスタム                               | カスタム。                           |
### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

| 変数                               | 説明                           |
|:-----------------------------------|:-------------------------------|
| 全てのイベント                     | 全てのイベント。               |
| `page.display`                     | ページ表示。                   |
| `click.action`                     | クリックアクション。           |
| `click.navigation`                 | クリックナビゲーション。       |
| `click.download`                   | クリックダウンロード。         |
| `click.exit`                       | クリック終了。                 |
| `publisher.impression`             | パブリッシャーインプレッション。 |
| `publisher.click`                  | パブリッシャークリック。       |
| `self_promotion.impression`        | セルフプロモーションインプレッション。 |
| `self_promotion.click`             | セルフプロモーションクリック。 |
| `internal_search_result.display`   | 内部検索結果表示。             |
| `internal_search_result.click`     | 内部検索結果クリック。         |
| `mv_test.display`                  | MVテスト表示。                 |
| `product.display`                  | 商品表示。                     |
| `product.page_display`             | 商品ページ表示。               |
| `product.add_to_cart`              | カートに商品を追加。           |
| `product.remove_from_cart`         | カートから商品を削除。         |
| `product.awaiting_payment`         | 支払い待ちの商品。             |
| `product.purchased`                | 購入された商品。               |
| `cart.creation`                    | カート作成。                   |
| `cart.display`                     | カート表示。                   |
| `cart.update`                      | カート更新。                   |
| `cart.delivery`                    | カート配送。                   |
| `cart.payment`                     | カート支払い。                 |
| `cart.awaiting_payment`            | 支払い待ちのカート。           |
| `transaction.confirmation`         | 取引確認。                     |
| `setUser`                          | ユーザー構成。                 |
| `getUser`                          | ユーザー取得。                 |
| `deleteUser`                       | ユーザー削除。                 |
| `getSessionID`                     | セッションID取得。             |
| `av.play`                          | AV再生。                       |
| `av.buffer.start`                  | AVバッファ開始。               |
| `av.buffer.heartbeat`              | AVバッファハートビート。       |
| `av.start`                         | AV開始。                       |
| `av.heartbeat`                     | AVハートビート。               |
| `av.pause`                         | AV一時停止。                   |
| `av.rebuffer.start`                | AVリバッファ開始。             |
| `av.rebuffer.heartbeat`            | AVリバッファハートビート。     |
| `av.resume`                        | AV再開。                       |
| `av.stop`                          | AV停止。                       |
| `av.seek.start`                    | AVシーク開始。                 |
| `av.forward`                       | AV早送り。                     |
| `av.backward`                      | AV巻き戻し。                   |
| `av.ad.click`                      | AV広告クリック。               |
| `av.ad.skip`                       | AV広告スキップ。               |
| `av.error`                         | AVエラー。                     |
| `av.display`                       | AV表示。                       |
| `av.close`                         | AV閉じる。                     |
| `av.volume`                        | AV音量。                       |
| `av.subtitle.on`                   | AV字幕オン。                   |
| `av.subtitle.off`                  | AV字幕オフ。                   |
| `av.fullscreen.on`                 | AV全画面オン。                 |
| `av.fullscreen.off`                | AV全画面オフ。                 |
| `av.quality`                       | AV品質。                       |
| `av.speed`                         | AV速度。                       |
| `av.share`                         | AV共有。                       |
| カスタム                           | カスタム。                     |
