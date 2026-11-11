---
title: Spotify Pixelタグ構成ガイド
description: この記事では、タグ管理アカウントでSpotify Pixelタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/spotify-pixel-tag/
---
この記事では、Spotify Pixelタグを構成する方法について説明します。

Spotifyは、ホスティングプロバイダーを横断してリアルタイムで透明性の高いインプレッションレポートを提供します。これにより、広告主はキャンペーンの進捗状況やリーチしている世帯数を把握できます。Spotifyはポッドキャストのダウンロードとサイト上のアクティビティを関連付け、広告主とパブリッシャーにポッドキャスト広告キャンペーンの効果に関するこれまでにないインサイトを提供します。

## タグに関するヒント

* マッピングを使用して標準パラメータを上書きします。
* Eコマース拡張機能のパラメータがサポートされています。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときは、次の構成を行います。

* **Spotify Pixel ID**：クライアントごとに一意のSpotify Pixel ID

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `spotify_id` | 文字列 | Spotify Pixel ID |
| `value` | 数値 | 値 |
| `discount_code` | 文字列 | 割引コード |
| `category` | 文字列 | カテゴリー |
| `type` | 文字列 | タイプ |
| `id` | 文字列 | ハッシュ化された内部ID |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `order_id`（`_corder`を上書き） | 文字列 | 注文ID |
| `order_subtotal`（`_csubtotal`を上書き） | 文字列 | 注文小計 |
| `currency`（`_ccurrency`を上書き） | 文字列 | 注文通貨 |
| `order_coupon_code`（`_cpromo`を上書き） | 文字列 | 割引コード |
| `order_total`（`_ctotal`を上書き） | 文字列 | 注文合計 |
| `is_new_customer` | ブール値 | 新規顧客かどうか |
| `product_unit_price` | 数値の配列 | 商品単価 |
| `quantity` | 数値の配列 | 商品数量 |
| `product_id` | 配列 | 商品ID |
| `product_name` | 配列 | 商品名 |
| `product_type` | 配列 | 商品タイプ |
| `product_vendor` | 配列 | 商品ベンダー |
| `variant_id` | 配列 | バリエーションID |
| `variant_name` | 配列 | バリエーション名 |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `alias` | エイリアス |
| `lead` | リード |
| `product` | 商品 |
| `addtocart` | カートに追加 |
| `checkout` | チェックアウト |
| `purchase` | 購入 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `spotify_id` | Spotify Pixel ID |
| `value` | 値（`value`） |
| `discount_code` | 割引コード |
| `category` | カテゴリー |
| `type` | タイプ |
| `id` | ハッシュ化された内部ID |
| `order_id` | 注文ID |
| `order_subtotal` | 注文小計 |
| `currency` | 注文通貨 |
| `order_coupon_code` | 割引コード |
| `order_total` | 注文合計 |
| `is_new_customer` | 新規顧客かどうか |
| `product_unit_price` | 商品単価 |
| `quantity` | 商品数量 |
| `product_id` | 商品ID |
| `product_name` | 商品名 |
| `product_type` | 商品タイプ |
| `product_vendor` | 商品ベンダー |
| `variant_id` | バリエーションID |
| `variant_name` | バリエーション名 |
| `alias` | エイリアス |
| `lead` | リード |
| `product` | 商品 |
| `addtocart` | カートに追加 |
| `checkout` | チェックアウト |
| `purchase` | 購入 |