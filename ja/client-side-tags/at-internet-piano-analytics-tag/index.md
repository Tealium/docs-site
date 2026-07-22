---
title: AT Internet Piano Analytics タグの構成ガイド
description: この記事では、Tealium Tag Management アカウントで AT Internet Piano Analytics タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/at-internet-piano-analytics-tag/
---
Piano Analytics は、Analytics Suite 2 の論理的な進化です。このソリューションは、20年以上にわたり継続的に開発され、数万人の顧客に支持されてきました。Piano Analytics は、ユーザー中心、倫理的な設計、価値志向のデータモデルを持ち、業界が直面する深刻なデータ品質の問題を解決します。

## タグのヒント

* マッピングを使用して、標準の構成値を動的に上書きします。

## タグの構成

新しいタグを追加するために、タグマーケットプレイスに移動します。タグを追加する方法の一般的な手順については、[タグの概要](https://docs.tealium.com/about-tags/) 記事を参照してください。

タグを追加する際に、以下の構成を構成します：

* **サイト ID**: AT Internet サイト ID。
* **コレクションドメイン**: AT Internet データ収集ドメイン。
* **コレクションパス**: AT Internet ピクセルリクエストの URL パス。
* **イベント URL を追加**: 現在のページの URL を含む `page_url` プロパティをすべてのイベントに自動的に追加します。 (デフォルトは `withoutQS` に構成されています)
* **オプトアウト時にイベントを送信する**: オプトアウト時にイベントを送信しますか？ (デフォルトは `true` です)
* **キャンペーンプレフィックス**: 収集するキャンペーンのタイプを優先順位付けして選択します。
* **UTM トラッキングを有効にする**: UTM パラメータをプロパティとして収集します。 (デフォルトは `true` です)
* **キュー名**: `_pac` からデフォルトの `queueName` を上書きするためにこのフィールドを使用します。

## ロードルール

タグをすべてのページで読み込むか、タグが読み込まれる条件を構成します。ロードルールについての詳細は、[ロードルール](https://docs.tealium.com/about-load-rules/) のドキュメントを参照してください。

## データマッピング

マッピングとは、データレイヤー変数からベンダータグの対応する変数にデータを送信するプロセスです。変数をタグの宛先にマッピングする方法についての手順は、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/) を参照してください。

利用可能なカテゴリは次のとおりです：

### タグの構成パラメータ

| 変数                                       | 説明 |
|:-----------------------------------------------|:------------|
| サイト ID (`site`)                               | [文字列]    |
| コレクションドメイン (`collectionDomain`)         | [文字列]    |
| コレクションパス (`collectionPath`)             | [文字列]    |
| イベント URL を追加 (`addEventURL`)                  | [真偽値]   |
| オプトアウト時にイベントを送信する (`sendEventWhenOptout`) | [真偽値]   |
| キャンペーンプレフィックス (`campaignPrefix`)             | [文字列]    |
| UTM トラッキングを有効にする (`enableUTMTracking`)      | [真偽値]   |
| キュー名 (`queueName`)                       | [文字列]    |

### コンバージョンパラメータ

| 変数                | 説明 |
|:------------------------|:------------|
| ゴールタイプ (`goal_type`) | [文字列]    |

### ページパラメータ

| 変数                         | 説明 |
|:---------------------------------|:------------|
| ページ (`page`)                    | [文字列]    |
| ページチャプター 1 (`page_chapter1`) | [文字列]    |
| ページチャプター 2 (`page_chapter2`) | [文字列]    |
| ページチャプター 3 (`page_chapter3`) | [文字列]    |

### クリックパラメータ

| 変数                           | 説明 |
|:-----------------------------------|:------------|
| クリック (`click`)                    | [文字列]    |
| クリックチャプター 1 (`click_chapter1`) | [文字列]    |
| クリックチャプター 2 (`click_chapter2`) | [文字列]    |
| クリックチャプター 3 (`click_chapter3`) | [文字列]    |

### オンサイト広告パラメータ

| 変数                                                      | 説明 |
|:--------------------------------------------------------------|:------------|
| オンサイト広告タイプ (必須) (`onsitead_type`)                  | [文字列]    |
| オンサイト広告広告主 (`onsitead_advertiser`)                 | [文字列]    |
| オンサイト広告キャンペーン (`onsitead_campaign`)                     | [文字列]    |
| オンサイト広告カテゴリ (`onsitead_category`)                     | [文字列]    |
| オンサイト広告作成 (`onsitead_creation`)                     | [文字列]    |
| オンサイト広告詳細配置 (`onsitead_detailed_placement`) | [文字列]    |
| オンサイト広告フォーマット (`onsitead_format`)                         | [文字列]    |
| オンサイト広告一般配置 (`onsitead_general_placement`)   | [文字列]    |
| オンサイト広告 URL (`onsitead_url`)                               | [文字列]    |
| オンサイト広告バリアント (`onsitead_variant`)                       | [文字列]    |

### 内部検索エンジンパラメータ

| 変数                          | 説明 |
|:----------------------------------|:------------|
| 内部検索エンジンのキーワード (`ise_keyword`)       | [文字列]    |
| 内部検索エンジンのページ (`ise_page`)             | [数値]    |
| 内部検索エンジンのクリック順位 (`ise_click_rank`) | [数値]    |

### MV テストパラメータ

| 変数                    | 説明 |
|:----------------------------|:------------|
| MV 作成 (`mv_creation`) | [文字列]    |
| MV テスト (`mv_test`)         | [文字列]    |
| MV ウェーブ (`mv_wave`)         | [数値]    |

### 商品パラメータ

| 変数                                                              | 説明        |
|:----------------------------------------------------------------------|:-------------------|
| 商品 ID (`product_id`) (Overrides `_cprod`)                        | [文字列の配列]  |
| 商品ラベル (`product`) (Overrides `_cprodname`)                    | [文字列の配列]  |
| 商品バリアント (`product_variant`)                                   | [文字列]           |
| 商品ブランド (`product_brand`) (Overrides `_cbrand`)                 | [文字列の配列]  |
| 割引商品? (`product_discount`) (Overrides `_cpdisc`)        | [真偽値の配列] |
| 税込価格 (`product_pricetaxincluded`) (Overrides `_cprice`) | [数値の配列]  |
| 税抜価格 (`product_pricetaxfree`)                               | [数値]           |
| 通貨 (ISO 4217) (`product_currency`)                              | [文字列]           |
| 在庫あり? (`product_stock`)                                   | [真偽値]          |
| 商品数量 (`product_quantity`) (Overrides `_cquan`)            | [数値の配列]  |
| レベル 1 カテゴリ (`product_category1`) (Overrides `_ccat`)            | [文字列の配列]  |
| レベル 2 カテゴリ (`product_category2`) (Overrides `_ccat2`)           | [文字列の配列]  |
| レベル 3 カテゴリ (`product_category3`)                                | [文字列]           |
| レベル 4 カテゴリ (`product_category4`)                                | [文字列]           |
| この商品追加によって作成されたカート? (`product_cartcreation`)       | [真偽値]          |

### カートパラメータ

| 変数                                                                | 説明 |
|:------------------------------------------------------------------------|:------------|
| カート ID (`cart_id`) (Overrides `_corder`)                               | [文字列]    |
| カート通貨 (`cart_currency`) (Overrides `_ccurrency`)                | [文字列]    |
| 税込売上 (`cart_turnovertaxincluded`)                      | [数値]    |
| 税抜売上 (`cart_turnovertaxfree`)                              | [数値]    |
| カート作成日 (タイムスタンプ UTC 秒単位) (`cart_creation_utc`)     | [数値]    |
| 商品数 (`cart_quantity`) (Overrides `_ctotal`)              | [数値]    |
| 異なる商品数 (`cart_nbdistinctproduct`)                  | [数値]    |
| カートに関連付けられた新しい一意のバージョン識別子 (`cart_version`) | [数値]    |

### トランザクションパラメータ

| 変数                                                      | 説明       |
|:--------------------------------------------------------------|:------------------|
| トランザクション ID (`transaction_id`)                             | [文字列]          |
| プロモーションコードリスト (`transaction_promocode`)                     | [文字列の配列] |
| 顧客の最初の購入? (`transaction_firstpurchase`) | [真偽値]         |

### 配送および支払いパラメータ

| 変数                                              | 説明 |
|:------------------------------------------------------|:------------|
| 配送タイプ (`shipping_delivery`)                     | [文字列]    |
| 税込配送料 (`shipping_costtaxincluded`) | [数値]    |
| 税抜配送料 (`shipping_costtaxfree`)         | [数値]    |
| 支払い方法 (`payment_mode`)                           | [文字列]    |

### ユーザーパラメータ

| 変数                       | 説明 |
|:-------------------------------|:------------|
| 訪問 ID (`visitorId`)  | カスタム訪問 ID (GUID または 16 文字) |
| ユーザー ID (`userId`)               | [文字列]    |
| ユーザーカテゴリ (`userCategory`)   | [文字列]    |
| 保存を有効にする (`enableStorage`) | [真偽値]   |

### グローバルパラメータ

| 変数                                                       | 説明 |
|:---------------------------------------------------------------|:------------|
| クッキーのドメイン (`cookieDomain`)                        | [文字列]    |
| クライアントサイドのクッキーの "SameSite" フラグ (`cookieSameSite`)     | [文字列]    |
| クライアントサイドのクッキーの "Secure" フラグ (`cookieSecure`) | [真偽値]   |
| 保存値のエンコード (`encodeStorageBase64`)                     | [真偽値]   |

### プライバシーと保存パラメータ

| 変数                                                                 | 説明 |
|:-------------------------------------------------------------------------|:------------|
| デフォルトのプライバシーモード (`privacyDefaultMode`)                             | [文字列]    |
| 保存のライフタイムプライバシー値 (`storageLifetimePrivacy`)                  | [数値]    |
| 保存のライフタイムユーザー値 (`storageLifetimeUser`)                        | [数値]    |
| 保存のライフタイム訪問値 (`storageLifetimeVisitor`)                  | [数値]    |
| 訪問のクッキーの相対または固定のライフタイム値 (`visitorStorageMode`) | [文字列]    |

### 訪問ポリシーパラメータ

| 変数                                                                    | 説明 |
|:----------------------------------------------------------------------------|:------------|
| クッキーのデポジットがクライアントサイドですか？ `false` の場合、サーバーサイド (`isVisitorClientSide`) | [真偽値]   |

### オーディオビデオパラメータ

| 変数                                                                                          | 説明        |
|:--------------------------------------------------------------------------------------------------|:-------------------|
| 再生のセッション ID                                                                        | [文字列]           |
| 再生中の 2 つのハートビート間の遅延時間、最小遅延時間は 5 秒 (`heartbeatDuration`)           | [数値またはオブジェクト] |
| バッファリング中の 2 つのハートビート間の遅延時間、最小遅延時間は 1 秒 (`bufferingHeartbeatDuration`) | [数値またはオブジェクト] |
| SDK によって生成されたセッション ID (`av_session_id`)                                                  | [文字列]           |
| コンテンツ ID (`av_content_id`)                                                                        | [文字列]           |
| コンテンツラベル (`av_content`)                                                                        | [文字列]           |
| コンテンツタイプ (`av_content_type`)                                                                    | [文字列]           |
| コンテンツの再生時間、ミリ秒単位 (`av_content_duration`)                                           | [数値]           |
| 関連コンテンツラベル (`av_content_linked`)                                                          | [文字列]           |
| 公開日、タイムスタンプ (`av_publication_date`)                                                 | [数値]           |
| コンテンツのジャンル (`av_content_genre`)                                                                | [文字列の配列]  |
| ショーラベル (`av_show`)                                                                              | [文字列]           |
| ショーシーズンラベル (`av_show_season`)                                                                | [文字列]           |
| エピソード ID (`av_episode_id`)                                                                        | [文字列]           |
| エピソードラベル (`av_episode`)                                                                        | [文字列]           |
| チャンネルラベル (`av_channel`)                                                                        | [文字列]           |
| 著者名 (`av_author`)                                                                           | [文字列]           |
| コンテンツバージョン (`av_content_version`)                                                              | [文字列]           |
| 再生時間範囲 (`av_content_duration_range`)                                                        | [文字列]           |
| 放送タイプ (`av_broadcasting_type`)                                                          | [文字列]           |
| 放送局名 (`av_broadcaster`)                                                                 | [文字列]           |
| 広告タイプ (`av_ad_type`)                                                                              | [文字列]           |
| プレーヤーラベル (`av_player`)                                                                          | [文字列]           |
| プレーヤーバージョン (`av_player_version`)                                                                | [文字列]           |
| プレーヤーの位置 (`av_player_position`)                                                              | [文字列]           |
| 自動再生モード (`av_auto_mode`)                                                                     | [真偽値]          |
| メディアの言語 (`av_language`)                                                                      | [文字列]           |
| 字幕 (`av_subtitles`)                                                                          | [文字列]           |
| 起動理由 (`av_launch_reason`)                                                                  | [文字列]           |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/) を参照してください。

| 変数                       | 説明                    |
|:-------------------------------|:-------------------------------|
| `page.display`                   | page.display                   |
| `click.action`                   | click.action                   |
| `click.navigation`               | click.navigation               |
| `click.download`                 | click.download                 |
| `click.exit`                     | click.exit                     |
| `publisher.impression`           | publisher.impression           |
| `publisher.click`                | publisher.click                |
| `self_promotion.impression`      | self_promotion.impression      |
| `self_promotion.click`           | self_promotion.click           |
| `internal_search_result.display` | internal_search_result.display |
| `internal_search_result.click`   | internal_search_result.click   |
| `mv_test.display`                | mv_test.display                |
| `product.display`                | product.display                |
| `product.page_display`           | product.page_display           |
| `product.add_to_cart`            | product.add_to_cart            |
| `product.remove_from_cart`       | product.remove_from_cart       |
| `product.awaiting_payment`       | product.awaiting_payment       |
| `product.purchased`              | product.purchased              |
| `cart.creation`                  | cart.creation                  |
| `cart.display`                   | cart.display                   |
| `cart.update`                    | cart.update                    |
| `cart.delivery`                  | cart.delivery                  |
| `cart.payment`                   | cart.payment                   |
| `cart.awaiting_payment`          | cart.awaiting_payment          |
| `transaction.confirmation`       | transaction.confirmation       |
| `setUser`                        | setUser                        |
| `getUser`                        | getUser                        |
| `deleteUser`                     | deleteUser                     |
| `getSessionID`                   | getSessionID                   |
| `av.play`                        | av.play                        |
| `av.buffer.start`                | av.buffer.start                |
| `av.buffer.heartbeat`            | av.buffer.heartbeat            |
| `av.start`                       | av.start                       |
| `av.heartbeat`                   | av.heartbeat                   |
| `av.pause`                       | av.pause                       |
| `av.rebuffer.start`              | av.rebuffer.start              |
| `av.rebuffer.heartbeat`          | av.rebuffer.heartbeat          |
| `av.resume`                      | av.resume                      |
| `av.stop`                        | av.stop                        |
| `av.seek.start`                  | av.seek.start                  |
| `av.forward`                     | av.forward                     |
| `av.backward`                    | av.backward                    |
| `av.ad.click`                    | av.ad.click                    |
| `av.ad.skip`                     | av.ad.skip                     |
| `av.error`                       | av.error                       |
| `av.display`                     | av.display                     |
| `av.close`                       | av.close                       |
| `av.volume`                      | av.volume                      |
| `av.subtitle.on`                 | av.subtitle.on                 |
| `av.subtitle.off`                | av.subtitle.off                |
| `av.fullscreen.on`               | av.fullscreen.on               |
| `av.fullscreen.off`              | av.fullscreen.off              |
| `av.quality`                     | av.quality                     |
| `av.speed`                       | av.speed                       |
| `av.share`                       | av.share                       |
| カスタム                         | custom                         |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/) を参照してください。

| 変数                       | 説明                    |
|:-------------------------------|:-------------------------------|
| `page.display`                   | page.display                   |
| `click.action`                   | click.action                   |
| `click.navigation`               | click.navigation               |
| `click.download`                 | click.download                 |
| `click.exit`                     | click.exit                     |
| `publisher.impression`           | publisher.impression           |
| `publisher.click`                | publisher.click                |
| `self_promotion.impression`      | self_promotion.impression      |
| `self_promotion.click`           | self_promotion.click           |
| `internal_search_result.display` | internal_search_result.display |
| `internal_search_result.click`   | internal_search_result.click   |
| `mv_test.display`                | mv_test.display                |
| `product.display`                | product.display                |
| `product.page_display`           | product.page_display           |
| `product.add_to_cart`            | product.add_to_cart            |
| `product.remove_from_cart`       | product.remove_from_cart       |
| `product.awaiting_payment`       | product.awaiting_payment       |
| `product.purchased`              | product.purchased              |
| `cart.creation`                  | cart.creation                  |
| `cart.display`                   | cart.display                   |
| `cart.update`                    | cart.update                    |
| `cart.delivery`                  | cart.delivery                  |
| `cart.payment`                   | cart.payment                   |
| `cart.awaiting_payment`          | cart.awaiting_payment          |
| `transaction.confirmation`       | transaction.confirmation       |
| `setUser`                        | setUser                        |
| `getUser`                        | getUser                        |
| `deleteUser`                     | deleteUser                     |
| `getSessionID`                   | getSessionID                   |
| `av.play`                        | av.play                        |
| `av.buffer.start`                | av.buffer.start                |
| `av.buffer.heartbeat`            | av.buffer.heartbeat            |
| `av.start`                       | av.start                       |
| `av.heartbeat`                   | av.heartbeat                   |
| `av.pause`                       | av.pause                       |
| `av.rebuffer.start`              | av.rebuffer.start              |
| `av.rebuffer.heartbeat`          | av.rebuffer.heartbeat          |
| `av.resume`                      | av.resume                      |
| `av.stop`                        | av.stop                        |
| `av.seek.start`                  | av.seek.start                  |
| `av.forward`                     | av.forward                     |
| `av.backward`                    | av.backward                    |
| `av.ad.click`                    | av.ad.click                    |
| `av.ad.skip`                     | av.ad.skip                     |
| `av.error`                       | av.error                       |
| `av.display`                     | av.display                     |
| `av.close`                       | av.close                       |
| `av.volume`                      | av.volume                      |
| `av.subtitle.on`                 | av.subtitle.on                 |
| `av.subtitle.off`                | av.subtitle.off                |
| `av.fullscreen.on`               | av.fullscreen.on               |
| `av.fullscreen.off`              | av.fullscreen.off              |
| `av.quality`                     | av.quality                     |
| `av.speed`                       | av.speed                       |
| `av.share`                       | av.share                       |
| カスタム                         | custom                         |
