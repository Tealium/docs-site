---
title: Branch.ioタグ
description: この記事では、Tealium iQタグ管理アカウントでBranch.ioタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/branchio-tag/
---
Branchは、異なるデバイス、プラットフォーム、チャネル間でユーザーエクスペリエンスと測定を統一するソリューションを提供する、業界をリードするモバイルリンクプラットフォームを提供しています。

## タグの構成

まず、タグマーケットプレイスに移動し、Branch.ioタグを追加します（[タグの追加方法](https://docs.tealium.com/manage-tags/)について詳しくはこちら）。

タグを追加したら、以下の構成を行います：

* **Branchキー**：あなたのBranchライブキー、または（非推奨）あなたのアプリID。

## データマッピング

マッピングは、[データレイヤー変数](https://docs.tealium.com/data-layer-variables/)からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[データマッピング](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 初期

| 変数                                              | 説明 |
|:----------------------------------------------------|:------------|
| Branchキー                                          |             |
| BranchビューID (`branch_view_id`)                   | [文字列]    |
| BranchマッチID (`branch_match_id`)                  | [文字列]    |
| No Journeys (`no_journeys`)                         | [ブール値]   |
| エントリーアニメーションの無効化 (`disable_entry_animation`) | [ブール値]   |
| 退場アニメーションの無効化 (`disable_exit_animation`)   | [ブール値]   |
| 再試行 (`retries`)                                 | [整数]   |
| 再試行遅延 (`retry_delay`)                         | [整数]   |
| タイムアウト (`timeout`)                           | [整数]   |
| メタデータ (`metadata`)                             | [オブジェクト]    |
| ノンス (`nonce`)                                     | [文字列]    |
| トラッキング無効 (`tracking_disabled`)               | [ブール値]   |

### メタデータ

| 変数                                       | 説明 |
|:-----------------------------------------------|:------------|
| トランザクションID (`transaction_id`)              | [文字列]    |
| 通貨 (`currency`) (Overrides `_ccurrency`) | [文字列]    |
| 収益 (`revenue`) (Overrides `_ctotal`)      | [文字列]    |
| 配送 (`shipping`) (Overrides `_cship`)     | [文字列]    |
| 税 (`tax`) (Overrides `_ctax`)                | [文字列]    |
| クーポン (`coupon`) (Overrides `_cpromo`)        | [数値]    |
| 所属 (`affiliation`)                    | [数値]    |
| 説明 (`description`)                    | [配列]     |
| 購入場所 (`purchase_loc`)                  | [文字列]    |
| 店舗受け取り (`store_pickup`)                  | [オブジェクト]    |
| 登録ID (`registration_id`)            | [オブジェクト]    |
| 顧客イベントエイリアス (`customer_event_alias`)  | [文字列]    |

### E-コマース

| 変数                                                            | 説明     |
|:--------------------------------------------------------------------|:----------------|
| コンテンツスキーマ (`$content_schema`)                                  | [文字列]        |
| Ogタイトル (`$og_title`)                                              | [文字列]        |
| Og説明 (`$og_description`)                                  | [文字列]        |
| Og画像URL (`$og_image_url`)                                      | [文字列]        |
| 正規識別子 (`$canonical_identifier`) (Overrides `_cprod`) | [文字列]        |
| 公開可能 (`$publicly_indexable`)                          | [ブール値]       |
| 価格 (`$price`) (Overrides `_cprice`)                              | [数値, 配列] |
| ローカルにインデクシング可能 (`$locally_indexable`)                            | [ブール値]       |
| 数量 (`$quantity`) (Overrides `_cquan`)                         | [数値, 配列] |
| SKU (`$sku`) (Overrides `_csku`)                                    | [文字列, 配列] |
| 商品名 (`$product_name`) (Overrides `_cprodname`)             | [文字列, 配列] |
| 商品ブランド (`$product_brand`) (Overrides `_cbrand`)              | [文字列, 配列] |
| 商品カテゴリ (`$product_category`) (Overrides `_ccat`)          | [文字列, 配列] |
| 商品バリアント (`$product_variant`)                                | [文字列]        |
| レーティング平均 (`$rating_average`)                                  | [数値]        |
| レーティング数 (`$rating_count`)                                      | [数値]        |
| レーティング最大 (`$rating_max`)                                          | [数値]        |
| 作成タイムスタンプ (`$creation_timestamp`)                          | [数値]        |
| 有効期限 (`$exp_date`)                                              | [文字列]        |
| キーワード (`$keywords`)                                              | [配列]         |
| 住所（通り） (`$address_street`)                                  | [文字列]        |
| 住所（市区町村） (`$address_city`) (Overrides `_ccity`)                 | [文字列]        |
| 住所（地域） (`$address_region`) (Overrides `_cstate`)            | [文字列]        |
| 住所（国） (`$address_country`) (Overrides `_ccountry`)        | [文字列]        |
| 住所（郵便番号） (`$address_postal_code`) (Overrides `_czip`)    | [文字列]        |
| 緯度 (`$latitude`)                                              | [数値]        |
| 経度 (`$longitude`)                                            | [数値]        |
| 画像キャプション (`$image_captions`)                                  | [配列]         |
| 状態 (`$condition`)                                            | [文字列]        |
| カスタムフィールド (`$custom_fields`)                                    | [オブジェクト]        |

### イベント

| 変数              | 説明             |
|:----------------------|:------------------------|
| カートに追加           | `add_to_cart`           |
| ほしい物リストに追加       | `add_to_wishlist`       |
| カートを見る             | `view_cart`             |
| 購入を開始     | `initiate_purchase`     |
| 支払い情報を追加      | `add_payment_info`      |
| 広告をクリック              | `click_ad`              |
| 購入              | `purchase`              |
| 予約               | `reserve`               |
| クレジットを使う         | `spend_credits`         |
| 広告を見る               | `view_ad`               |
| 検索                | `search`                |
| アイテムを見る             | `view_item`             |
| アイテムを見る            | `view_items`            |
| 評価                  | `rate`                  |
| 共有                 | `share`                 |
| ストリームを開始       | `initiate_stream`       |
| ストリームを完了       | `complete_stream`       |
| 登録を完了 | `complete_registration` |
| チュートリアルを完了     | `complete_tutorial`     |
| レベルを達成         | `achieve_level`         |
| 実績を解除    | `unlock_achievement`    |
| 招待                | `invite`                |
| ログイン                 | `login`                 |
| トライアルを開始           | `start_trial`           |
| 購読             | `subscribe`             |
| カスタム                | `custom`                |

### イベントパラメータ

| 変数              | 説明             |
|:----------------------|:------------------------|
| カートに追加           | `add_to_cart`           |
| ほしい物リストに追加       | `add_to_wishlist`       |
| カートを見る             | `view_cart`             |
| 購入を開始     | `initiate_purchase`     |
| 支払い情報を追加      | `add_payment_info`      |
| 広告をクリック              | `click_ad`              |
| 購入              | `purchase`              |
| 予約               | `reserve`               |
| クレジットを使う         | `spend_credits`         |
| 広告を見る               | `view_ad`               |
| 検索                | `search`                |
| アイテムを見る             | `view_item`             |
| アイテムを見る            | `view_items`            |
| 評価                  | `rate`                  |
| 共有                 | `share`                 |
| ストリームを開始       | `initiate_stream`       |
| ストリームを完了       | `complete_stream`       |
| 登録を完了 | `complete_registration` |
| チュートリアルを完了     | `complete_tutorial`     |
| レベルを達成         | `achieve_level`         |
| 実績を解除    | `unlock_achievement`    |
| 招待                | `invite`                |
| ログイン                 | `login`                 |
| トライアルを開始           | `start_trial`           |
| 購読             | `subscribe`             |
| カスタム                | `custom`                |
