---
title: Piano Analyticsタグ構成ガイド
description: この記事では、タグ管理アカウントでPiano Analyticsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/piano-analytics-tag/
---
## タグに関するヒント

* マッピングを使用すると、標準の構成値を動的に上書きできます。
* **同意モードを構成**パラメータに指定できる値は、`opt-in`、`essential`、`opt-out`のみです。

このタグは、次のベンダーSDKに基づいています：[Piano Analytics：JavaScript](https://developers.atinternet-solutions.com/piano-analytics/data-collection/sdks/javascript)。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳しくは、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **サイトID**：AT InternetのサイトID。
* **収集ドメイン**：AT Internetのデータ収集ドメイン。
* **収集パス**：AT InternetのピクセルリクエストURLパス。
* **イベントURLを追加**：現在のページのURLを含む`page_url`プロパティを、すべてのイベントに自動的に追加します。デフォルト値は`withoutQS`です。
* **同意を必須にする**：同意機能を有効にするには、`requireConsent`変数を`true`に構成します。
* **オプトアウト時にイベントを送信**：オプトアウト時にイベントを送信するかどうかを指定します。デフォルト値は`true`です。
* **キャンペーンプレフィックス**：収集するキャンペーンのタイプを優先順位に従って選択します。
* **UTMトラッキングを有効にする**：UTMパラメータをプロパティとして収集します。デフォルト値は`true`です。
* **キュー名**：このフィールドを使用して、`_pac`のデフォルトの`queueName`を上書きします。
* **プライバシーのデフォルトモード**：プライバシーのデフォルトモードとして、`opt-in`、`essential`、`opt-out`のいずれかを選択します。
* **Tealium同意Cookieから自動的に読み取る**：Tealium Consent Managerと連携します。

## ロードルール

すべてのページでタグをロードするか、タグをロードする条件を構成します。ロードルールについて詳しくは、[ロードルール](https://docs.tealium.com/about-load-rules/)のドキュメントを参照してください。

## データマッピング

データマッピングでは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳しくは、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### タグ構成パラメータ

| 変数                      | 型        | 説明                         |
|:--------------------------|:----------|:-----------------------------|
| `site`                    | 文字列    | サイトID。                   |
| `collectionDomain`        | 文字列    | 収集ドメイン。               |
| `collectionPath`          | 文字列    | 収集パス。                   |
| `addEventURL`             | ブール値  | イベントURLを追加します。    |
| `sendEventWhenOptout`     | ブール値  | オプトアウト時にイベントを送信します。 |
| `campaignPrefix`          | 文字列    | キャンペーンプレフィックス。 |
| `enableUTMTracking`       | ブール値  | UTMトラッキングを有効にします。 |
| `queueName`               | 文字列    | キュー名。                   |

### コンバージョンパラメータ

| 変数        | 型       | 説明           |
|:------------|:---------|:---------------|
| `goal_type` | 文字列   | ゴールタイプ。 |

### ページパラメータ

| 変数            | 型      | 説明               |
|:----------------|:--------|:-------------------|
| `page`          | 文字列  | ページ。           |
| `page_chapter1` | 文字列  | ページチャプター1。 |
| `page_chapter2` | 文字列  | ページチャプター2。 |
| `page_chapter3` | 文字列  | ページチャプター3。 |

### クリックパラメータ

| 変数              | 型      | 説明                 |
|:------------------|:--------|:---------------------|
| `click`           | 文字列  | クリック。           |
| `click_chapter1`  | 文字列  | クリックチャプター1。 |
| `click_chapter2`  | 文字列  | クリックチャプター2。 |
| `click_chapter3`  | 文字列  | クリックチャプター3。 |

### オンサイト広告パラメータ

| 変数                            | 型      | 説明                           |
|:--------------------------------|:--------|:-------------------------------|
| `onsitead_type`（必須）         | 文字列  | オンサイト広告のタイプ。       |
| `onsitead_advertiser`           | 文字列  | オンサイト広告の広告主。       |
| `onsitead_campaign`             | 文字列  | オンサイト広告のキャンペーン。 |
| `onsitead_category`             | 文字列  | オンサイト広告のカテゴリー。   |
| `onsitead_creation`             | 文字列  | オンサイト広告のクリエイティブ。 |
| `onsitead_detailed_placement`   | 文字列  | オンサイト広告の詳細な配置。   |
| `onsitead_format`               | 文字列  | オンサイト広告の形式。         |
| `onsitead_general_placement`    | 文字列  | オンサイト広告の一般的な配置。 |
| `onsitead_url`                  | 文字列  | オンサイト広告のURL。          |
| `onsitead_variant`              | 文字列  | オンサイト広告のバリエーション。 |

### ISE（内部検索エンジン）パラメータ

| 変数             | 型      | 説明                 |
|:-----------------|:--------|:---------------------|
| `ise_keyword`    | 文字列  | ISEキーワード。      |
| `ise_page`       | 数値    | ISEページ。          |
| `ise_click_rank` | 数値    | ISEクリック順位。    |

### MV（多変量）テストパラメータ

| 変数          | 型      | 説明                         |
|:--------------|:--------|:-----------------------------|
| `mv_creation` | 文字列  | 多変量クリエイティブ。       |
| `mv_test`     | 文字列  | 多変量テスト。               |
| `mv_wave`     | 数値    | 多変量ウェーブ。             |

### 製品パラメータ

| 変数                                              | 型                | 説明                                           |
|:--------------------------------------------------|:------------------|:-----------------------------------------------|
| `product_id`（`_cprod`を上書き）                  | 文字列の配列      | 製品ID。                                       |
| `product`（`_cprodname`を上書き）                 | 文字列の配列      | 製品ラベル。                                   |
| `product_variant`                                 | 文字列            | 製品バリエーション。                           |
| `product_brand`（`_cbrand`を上書き）              | 文字列の配列      | 製品ブランド。                                 |
| `product_discount`（`_cpdisc`を上書き）           | ブール値の配列    | 製品が廃止されているかどうか。                 |
| `product_pricetaxincluded`（`_cprice`を上書き）   | 数値の配列        | 税込み価格。                                   |
| `product_pricetaxfree`                            | 数値              | 税抜き価格。                                   |
| `product_currency`                                | 文字列            | 通貨（ISO 4217）。                             |
| `product_stock`                                   | ブール値          | 製品に在庫があるかどうか。                     |
| `product_quantity`（`_cquan`を上書き）            | 数値の配列        | 製品数量。                                     |
| `product_category1`（`_ccat`を上書き）            | 文字列の配列      | レベル1カテゴリー。                            |
| `product_category2`（`_ccat2`を上書き）           | 文字列の配列      | レベル2カテゴリー。                            |
| `product_category3`                               | 文字列            | レベル3カテゴリー。                            |
| `product_category4`                               | 文字列            | レベル4カテゴリー。                            |
| `product_cartcreation`                            | ブール値          | この製品の追加によってカートが作成されたかどうか。 |
### カートパラメータ

| 変数                                     | 型     | 説明                                                    |
|:-----------------------------------------|:-------|:--------------------------------------------------------|
| `cart_id`（`_corder` を上書き）          | 文字列 | カートID。                                              |
| `cart_currency`（`_ccurrency` を上書き） | 文字列 | カートの通貨。                                          |
| `cart_turnovertaxincluded`               | 数値   | 税込み売上高。                                          |
| `cart_turnovertaxfree`                   | 数値   | 税抜き売上高。                                          |
| `cart_creation_utc`                      | 数値   | UTC秒単位のカート作成日時。                             |
| `cart_quantity`（`_ctotal` を上書き）    | 数値   | 商品数。                                                |
| `cart_nbdistinctproduct`                 | 数値   | 異なる商品の数。                                        |
| `cart_version`                           | 数値   | カートに関連付けられた新しい一意のバージョン識別子。    |

### トランザクションパラメータ

| 変数                        | 型           | 説明                                             |
|:----------------------------|:-------------|:-------------------------------------------------|
| `transaction_id`            | 文字列       | トランザクションID。                             |
| `transaction_promocode`     | 文字列の配列 | プロモーションコードのリスト。                   |
| `transaction_firstpurchase` | ブール値     | 顧客による初回購入かどうか。                     |

### 配送および支払いパラメータ

| 変数                       | 型     | 説明                   |
|:---------------------------|:-------|:-----------------------|
| `shipping_delivery`        | 文字列 | 配送タイプ。           |
| `shipping_costtaxincluded` | 数値   | 税込み配送料。         |
| `shipping_costtaxfree`     | 数値   | 税抜き配送料。         |
| `payment_mode`             | 文字列 | 支払い方法。           |

### ユーザーパラメータ

| 変数            | 型         | 説明                                               |
|:----------------|:-----------|:---------------------------------------------------|
| `visitorId`     | 文字列     | カスタム訪問ID（GUIDまたは16文字）。             |
| `userId`        | 文字列     | ユーザーID。                                       |
| `userCategory`  | 文字列     | ユーザーカテゴリ。                                 |
| `enableStorage` | ブール値   | 保存を有効にするかどうか。                   |

### グローバルパラメータ

| 変数                  | 型         | 説明                                                                  |
|:----------------------|:-----------|:----------------------------------------------------------------------|
| `cookieDomain`        | 文字列     | 分析スクリプトによって構成されるトラッキングCookieのドメイン範囲。    |
| `cookieSameSite`      | 文字列     | クライアント側Cookieの **SameSite** フラグ。                           |
| `cookieSecure`        | ブール値   | クライアント側Cookieの **Secure** フラグ。                             |
| `encodeStorageBase64` | ブール値   | CookieがBase64でエンコードされるかどうか。                             |

### プライバシーおよび保存パラメータ

| 変数                     | 型         | 説明                                                     |
|:-------------------------|:-----------|:---------------------------------------------------------|
| `privacyDefaultMode`     | 文字列     | デフォルトのプライバシーモード。                         |
| `mode`                   | 文字列     | 同意モード。                                             |
| `requireConsent`         | 文字列     | 同意を必須にするかどうか。                               |
| `tealium_consent`        | ブール値   | Tealiumの同意。                                          |
| `properties`             | オブジェクト | プロパティの優先度構成。                               |
| `consent_events`         | オブジェクト | イベントの優先度構成。                                 |
| `storageLifetimePrivacy` | 数値       | プライバシーデータの保存有効期間値。               |
| `storageLifetimeUser`    | 数値       | ユーザーデータの保存有効期間値。                   |
| `storageLifetimeVisitor` | 数値       | 訪問データの保存有効期間値。                     |
| `visitorStorageMode`     | 文字列     | 訪問Cookieの相対または固定の有効期間値。               |

### 訪問ポリシーパラメータ

| 変数                   | 型       | 説明 |
|:-----------------------|:---------|:-----|
| `isVisitorClientSide` | ブール値 | 訪問IDがブラウザのCookieに保存されるかどうか。<ul><li>`true`：訪問IDはブラウザで生成され、保存されます。</li><li>`false`：訪問IDはサーバーによって管理されます。</li></ul> |

### オーディオ・ビデオパラメータ

| 変数                         | 型                     | 説明                                                               |
|:-----------------------------|:-----------------------|:-------------------------------------------------------------------|
| 再生セッションID             | 文字列                 | 再生のセッションID。                                               |
| `heartbeatDuration`          | 数値またはオブジェクト | 再生中の2回のハートビート間の時間。最小間隔は5秒です。             |
| `bufferingHeartbeatDuration` | 数値またはオブジェクト | バッファリング中の2回のハートビート間の時間。最小間隔は1秒です。   |
| `av_session_id`              | 文字列                 | SDKによって生成されるセッションID。                                |
| `av_content_id`              | 文字列                 | コンテンツID。                                                      |
| `av_content`                 | 文字列                 | コンテンツラベル。                                                  |
| `av_content_type`            | 文字列                 | コンテンツタイプ。                                                  |
| `av_content_duration`        | 数値                   | コンテンツの長さ（ミリ秒単位）。                                    |
| `av_content_linked`          | 文字列                 | 関連コンテンツのラベル。                                            |
| `av_publication_date`        | 数値                   | 公開日時（タイムスタンプ）。                                        |
| `av_content_genre`           | 文字列の配列           | コンテンツのジャンル。                                              |
| `av_show`                    | 文字列                 | 番組ラベル。                                                        |
| `av_show_season`             | 文字列                 | 番組シーズンのラベル。                                              |
| `av_episode_id`              | 文字列                 | エピソードID。                                                      |
| `av_episode`                 | 文字列                 | エピソードラベル。                                                  |
| `av_channel`                 | 文字列                 | チャンネルラベル。                                                  |
| `av_author`                  | 文字列                 | 作成者名。                                                          |
| `av_content_version`         | 文字列                 | コンテンツのバージョン。                                            |
| `av_content_duration_range`  | 文字列                 | 再生時間の範囲。                                                    |
| `av_broadcasting_type`       | 文字列                 | 放送タイプ。                                                        |
| `av_broadcaster`             | 文字列                 | 放送事業者名。                                                      |
| `av_ad_type`                 | 文字列                 | 広告タイプ。                                                        |
| `av_player`                  | 文字列                 | プレーヤーラベル。                                                  |
| `av_player_version`          | 文字列                 | プレーヤーのバージョン。                                            |
| `av_player_position`         | 文字列                 | プレーヤーの位置。                                                  |
| `av_auto_mode`               | ブール値               | 自動再生モード。                                                    |
| `av_language`                | 文字列                 | メディアの言語。                                                    |
| `av_subtitles`               | 文字列                 | 字幕。                                                              |
| `av_launch_reason`           | 文字列                 | 起動理由。                                                          |
### トラフィックソース

| 変数                 | 型     | 説明                       |
|:---------------------|:-------|:---------------------------|
| `src`                | 文字列 | ソース。                   |
| `src_details`        | 文字列 | ソースの詳細。             |
| `src_type`           | 文字列 | キャンペーンの自然流入。   |
| `src_medium`         | 文字列 | キャンペーンタイプ。       |
| `src_campaign`       | 文字列 | キャンペーン名。           |
| `src_se_category`    | 文字列 | 検索エンジンのカテゴリー。 |
| `src_portal_site_id` | 文字列 | ポータルサイト ID。        |

### エンリッチメントされたマーケティングソース検出

| 変数                      | 型      | 説明                       |
|:--------------------------|:--------|:---------------------------|
| `src_content`             | 文字列  | ソースコンテンツ。         |
| `src_creative_format`     | 文字列  | クリエイティブ形式。       |
| `src_id`                  | 文字列  | ソース ID。                |
| `src_marketing_tactic`    | 文字列  | マーケティング施策。       |
| `src_source`              | 文字列  | ソース。                   |
| `src_source_platform`     | 文字列  | ソースプラットフォーム。   |
| `src_term`                | 文字列  | ソースの語句。             |
| `event_collection_auto`   | ブール値 | イベントの自動収集。       |
| `geo_country_code_alpha2` | 文字列  | 国。                       |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

| 変数                             | 説明                               |
|:---------------------------------|:-----------------------------------|
| `page.display`                   | ページ表示。                       |
| `click.action`                   | クリックアクション。               |
| `click.navigation`               | ナビゲーションのクリック。         |
| `click.download`                 | ダウンロードのクリック。           |
| `click.exit`                     | 離脱のクリック。                   |
| `publisher.impression`           | パブリッシャーのインプレッション。 |
| `publisher.click`                | パブリッシャーのクリック。         |
| `self_promotion.impression`      | 自社プロモーションの表示。         |
| `self_promotion.click`           | 自社プロモーションのクリック。     |
| `internal_search_result.display` | 内部検索結果の表示。               |
| `internal_search_result.click`   | 内部検索結果の表示。               |
| `mv_test.display`                | MV テストの表示。                  |
| `product.display`                | 商品の表示。                       |
| `product.page_display`           | 商品ページの表示。                 |
| `product.add_to_cart`            | 商品をカートに追加。               |
| `product.remove_from_cart`       | 商品をカートから削除。             |
| `product.awaiting_payment`       | 商品の支払い待ち。                 |
| `product.purchased`              | 商品を購入済み。                   |
| `cart.creation`                  | カートを作成。                     |
| `cart.display`                   | カートの表示。                     |
| `cart.update`                    | カートを更新。                     |
| `cart.delivery`                  | カートの配送。                     |
| `cart.payment`                   | カートの支払い。                   |
| `cart.awaiting_payment`          | カートの支払い待ち。               |
| `transaction.confirmation`       | トランザクションの確認。           |
| `setUser`                        | ユーザーを構成。                   |
| `getUser`                        | ユーザーを取得。                   |
| `deleteUser`                     | ユーザーを削除。                   |
| `getSessionID`                   | セッション ID を取得。             |
| `av.play`                        | AV の再生。                        |
| `av.buffer.start`                | AV のバッファリング開始。          |
| `av.buffer.heartbeat`            | AV バッファのハートビート。        |
| `av.start`                       | AV の開始。                        |
| `av.heartbeat`                   | AV のハートビート。                |
| `av.pause`                       | AV の一時停止。                    |
| `av.rebuffer.start`              | AV の再バッファリング開始。        |
| `av.rebuffer.heartbeat`          | AV 再バッファリングのハートビート。|
| `av.resume`                      | AV の再開。                        |
| `av.stop`                        | AV の停止。                        |
| `av.seek.start`                  | AV のシーク開始。                  |
| `av.forward`                     | AV の早送り。                      |
| `av.backward`                    | AV の巻き戻し。                    |
| `av.ad.click`                    | AV 広告のクリック。                |
| `av.ad.skip`                     | AV 広告のスキップ。                |
| `av.error`                       | AV のエラー。                      |
| `av.display`                     | AV の表示。                        |
| `av.close`                       | AV を閉じる。                      |
| `av.volume`                      | AV の音量。                        |
| `av.subtitle.on`                 | AV の字幕をオン。                  |
| `av.subtitle.off`                | AV の字幕をオフ。                  |
| `av.fullscreen.on`               | AV の全画面表示をオン。            |
| `av.fullscreen.off`              | AV の全画面表示をオフ。            |
| `av.quality`                     | AV の品質。                        |
| `av.speed`                       | AV の再生速度。                    |
| `av.share`                       | AV の共有。                        |
| `set.mode`                       | モードを構成。                     |
| `get.mode`                       | モードを取得。                     |
| `disableconsent`                 | 同意を無効化。`mode` を `opt-out` に構成。 |
| カスタム                         | カスタム。                         |
### イベント固有のパラメーター

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/)を参照してください。

| 変数                             | 説明                                  |
|:---------------------------------|:--------------------------------------|
| すべてのイベント                 | すべてのイベント。                    |
| `page.display`                   | ページ表示。                          |
| `click.action`                   | クリックアクション。                  |
| `click.navigation`               | ナビゲーションクリック。              |
| `click.download`                 | ダウンロードクリック。                |
| `click.exit`                     | 離脱クリック。                        |
| `publisher.impression`           | パブリッシャーのインプレッション。    |
| `publisher.click`                | パブリッシャーのクリック。            |
| `self_promotion.impression`      | セルフプロモーションのインプレッション。 |
| `self_promotion.click`           | セルフプロモーションのクリック。      |
| `internal_search_result.display` | 内部検索結果の表示。                  |
| `internal_search_result.click`   | 内部検索結果の表示。                  |
| `mv_test.display`                | MVテストの表示。                      |
| `product.display`                | 商品の表示。                          |
| `product.page_display`           | 商品ページの表示。                    |
| `product.add_to_cart`            | 商品をカートに追加。                  |
| `product.remove_from_cart`       | 商品をカートから削除。                |
| `product.awaiting_payment`       | 商品の支払い待ち。                    |
| `product.purchased`              | 商品の購入。                          |
| `cart.creation`                  | カートの作成。                        |
| `cart.display`                   | カートの表示。                        |
| `cart.update`                    | カートの更新。                        |
| `cart.delivery`                  | カートの配送。                        |
| `cart.payment`                   | カートの支払い。                      |
| `cart.awaiting_payment`          | カートの支払い待ち。                  |
| `transaction.confirmation`       | トランザクションの確認。              |
| `setUser`                        | ユーザーを構成。                      |
| `getUser`                        | ユーザーを取得。                      |
| `deleteUser`                     | ユーザーを削除。                      |
| `getSessionID`                   | セッションIDを取得。                  |
| `av.play`                        | AVの再生。                            |
| `av.buffer.start`                | AVのバッファリング開始。              |
| `av.buffer.heartbeat`            | AVのバッファリングハートビート。      |
| `av.start`                       | AVの開始。                            |
| `av.heartbeat`                   | AVのハートビート。                    |
| `av.pause`                       | AVの一時停止。                        |
| `av.rebuffer.start`              | AVの再バッファリング開始。            |
| `av.rebuffer.heartbeat`          | AVの再バッファリングハートビート。    |
| `av.resume`                      | AVの再開。                            |
| `av.stop`                        | AVの停止。                            |
| `av.seek.start`                  | AVのシーク開始。                      |
| `av.forward`                     | AVの早送り。                          |
| `av.backward`                    | AVの巻き戻し。                        |
| `av.ad.click`                    | AV広告のクリック。                    |
| `av.ad.skip`                     | AV広告のスキップ。                    |
| `av.error`                       | AVのエラー。                          |
| `av.display`                     | AVの表示。                            |
| `av.close`                       | AVを閉じる。                          |
| `av.volume`                      | AVの音量。                            |
| `av.subtitle.on`                 | AVの字幕をオンにする。                |
| `av.subtitle.off`                | AVの字幕をオフにする。                |
| `av.fullscreen.on`               | AVの全画面表示をオンにする。          |
| `av.fullscreen.off`              | AVの全画面表示をオフにする。          |
| `av.quality`                     | AVの品質。                            |
| `av.speed`                       | AVの再生速度。                        |
| `av.share`                       | AVの共有。                            |
| カスタム                         | カスタム。                            |