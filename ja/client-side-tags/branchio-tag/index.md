---
title: Branch.ioタグ
description: この記事では、タグ管理アカウントでBranch.ioタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/branchio-tag/
---

Branchは、さまざまなデバイス、プラットフォーム、チャネルを横断してユーザーエクスペリエンスと測定を統合するソリューションを備えた、業界をリードするモバイルリンクプラットフォームを提供しています。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、次の構成を構成します。

* **Branchキー**：Branchのライブキー、または（非推奨の）アプリID。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 初期構成

| 変数                                                | 説明       |
|:----------------------------------------------------|:-----------|
| Branchキー                                          |            |
| BranchビューID（`branch_view_id`）                  | [文字列]   |
| Branch一致ID（`branch_match_id`）                   | [文字列]   |
| Journeysなし（`no_journeys`）                       | [ブール値] |
| 開始アニメーションを無効化（`disable_entry_animation`） | [ブール値] |
| 終了アニメーションを無効化（`disable_exit_animation`） | [ブール値] |
| 再試行回数（`retries`）                             | [整数]     |
| 再試行遅延（`retry_delay`）                         | [整数]     |
| タイムアウト（`timeout`）                           | [整数]     |
| メタデータ（`metadata`）                            | [オブジェクト] |
| Nonce（`nonce`）                                    | [文字列]   |
| トラッキング無効（`tracking_disabled`）             | [ブール値] |

### メタデータ

| 変数                                           | 説明             |
|:-----------------------------------------------|:-----------------|
| トランザクションID（`transaction_id`）         | [文字列]         |
| 通貨（`currency`）（`_ccurrency`を上書き）     | [文字列]         |
| 収益（`revenue`）（`_ctotal`を上書き）         | [文字列]         |
| 送料（`shipping`）（`_cship`を上書き）         | [文字列]         |
| 税（`tax`）（`_ctax`を上書き）                 | [文字列]         |
| クーポン（`coupon`）（`_cpromo`を上書き）      | [数値]           |
| アフィリエーション（`affiliation`）            | [数値]           |
| 説明（`description`）                          | [配列]           |
| 購入場所（`purchase_loc`）                     | [文字列]         |
| 店舗受け取り（`store_pickup`）                 | [オブジェクト]   |
| 登録ID（`registration_id`）                    | [オブジェクト]   |
| 顧客イベントエイリアス（`customer_event_alias`） | [文字列]       |

### Eコマース

| 変数                                                                | 説明         |
|:--------------------------------------------------------------------|:-------------|
| コンテンツスキーマ（`$content_schema`）                             | [文字列]     |
| OGタイトル（`$og_title`）                                           | [文字列]     |
| OG説明（`$og_description`）                                         | [文字列]     |
| OG画像URL（`$og_image_url`）                                        | [文字列]     |
| 正規識別子（`$canonical_identifier`）（`_cprod`を上書き）           | [文字列]     |
| 公開インデックス登録可能（`$publicly_indexable`）                   | [ブール値]   |
| 価格（`$price`）（`_cprice`を上書き）                               | [数値、配列] |
| ローカルインデックス登録可能（`$locally_indexable`）                | [ブール値]   |
| 数量（`$quantity`）（`_cquan`を上書き）                             | [数値、配列] |
| SKU（`$sku`）（`_csku`を上書き）                                    | [文字列、配列] |
| 商品名（`$product_name`）（`_cprodname`を上書き）                   | [文字列、配列] |
| 商品ブランド（`$product_brand`）（`_cbrand`を上書き）               | [文字列、配列] |
| 商品カテゴリー（`$product_category`）（`_ccat`を上書き）            | [文字列、配列] |
| 商品バリエーション（`$product_variant`）                            | [文字列]     |
| 平均評価（`$rating_average`）                                       | [数値]       |
| 評価数（`$rating_count`）                                           | [数値]       |
| 最大評価（`$rating_max`）                                           | [数値]       |
| 作成タイムスタンプ（`$creation_timestamp`）                         | [数値]       |
| 有効期限（`$exp_date`）                                             | [文字列]     |
| キーワード（`$keywords`）                                          | [配列]       |
| 住所（番地）（`$address_street`）                                   | [文字列]     |
| 住所（市区町村）（`$address_city`）（`_ccity`を上書き）             | [文字列]     |
| 住所（地域）（`$address_region`）（`_cstate`を上書き）              | [文字列]     |
| 住所（国）（`$address_country`）（`_ccountry`を上書き）             | [文字列]     |
| 住所（郵便番号）（`$address_postal_code`）（`_czip`を上書き）      | [文字列]     |
| 緯度（`$latitude`）                                                  | [数値]       |
| 経度（`$longitude`）                                                | [数値]       |
| 画像キャプション（`$image_captions`）                               | [配列]       |
| 状態（`$condition`）                                                | [文字列]     |
| カスタムフィールド（`$custom_fields`）                              | [オブジェクト] |

### イベント

| 変数                 | 説明                    |
|:---------------------|:------------------------|
| カートに追加         | `add_to_cart`           |
| ウィッシュリストに追加 | `add_to_wishlist`     |
| カートを表示         | `view_cart`             |
| 購入を開始           | `initiate_purchase`     |
| 支払い情報を追加     | `add_payment_info`      |
| 広告をクリック       | `click_ad`              |
| 購入                 | `purchase`              |
| 予約                 | `reserve`               |
| クレジットを使用     | `spend_credits`         |
| 広告を表示           | `view_ad`               |
| 検索                 | `search`                |
| アイテムを表示       | `view_item`             |
| 複数のアイテムを表示 | `view_items`            |
| 評価                 | `rate`                  |
| 共有                 | `share`                 |
| ストリーミングを開始 | `initiate_stream`       |
| ストリーミングを完了 | `complete_stream`       |
| 登録を完了           | `complete_registration` |
| チュートリアルを完了 | `complete_tutorial`     |
| レベルを達成         | `achieve_level`         |
| 実績を解除           | `unlock_achievement`    |
| 招待                 | `invite`                |
| ログイン             | `login`                 |
| トライアルを開始     | `start_trial`           |
| 購読                 | `subscribe`             |
| カスタム             | `custom`                |
### イベントパラメータ

| 変数                   | 説明                    |
|:----------------------|:------------------------|
| カートに追加           | `add_to_cart`           |
| ウィッシュリストに追加 | `add_to_wishlist`       |
| カートを表示           | `view_cart`             |
| 購入を開始             | `initiate_purchase`     |
| 支払い情報を追加       | `add_payment_info`      |
| 広告をクリック         | `click_ad`              |
| 購入                   | `purchase`              |
| 予約                   | `reserve`               |
| クレジットを使用       | `spend_credits`         |
| 広告を表示             | `view_ad`               |
| 検索                   | `search`                |
| アイテムを表示         | `view_item`             |
| 複数のアイテムを表示   | `view_items`            |
| 評価                   | `rate`                  |
| 共有                   | `share`                 |
| ストリームを開始       | `initiate_stream`       |
| ストリームを完了       | `complete_stream`       |
| 登録を完了             | `complete_registration` |
| チュートリアルを完了   | `complete_tutorial`     |
| レベルを達成           | `achieve_level`         |
| 実績を解除             | `unlock_achievement`    |
| 招待                   | `invite`                |
| ログイン               | `login`                 |
| トライアルを開始       | `start_Trial`           |
| 購読                   | `subscribe`             |
| カスタム               | `custom`                |