---
title: Spotify Pixel タグ構成ガイド
description: この記事では、Tealium iQ タグ管理アカウントでSpotify Pixel タグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/spotify-pixel-tag/
---
この記事では、Spotify Pixel タグの構成方法について説明します。

Spotifyは、広告主がキャンペーンの進行状況や到達している世帯数をリアルタイムで把握できるように、ホスティングプロバイダー間で透明なインプレッションレポートを提供します。Spotifyは、ポッドキャストのダウンロードをサイト上の活動と連携させ、広告主と公開社にポッドキャスト広告キャンペーンの効果について前例のない洞察を提供します。

## タグのヒント

* 標準パラメータを上書きするためにマッピングを使用します。
* サポートされているEコマース拡張パラメータ。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を構成します：

* **Spotify Pixel ID**：クライアントごとに一意のSpotify Pixel ID

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `spotify_id`  | 文字列 | Spotify Pixel ID |
|  `value`  | 数値 | 値 |
|  `discount_code`  | 文字列 | 割引コード | 
|  `category`  | 文字列 | カテゴリー |
|  `type`  | 文字列 | タイプ |
|  `id`  | 文字列 | ハッシュ化された内部ID | 

### Eコマース

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `order_id` (Overrides `_corder`)  | 文字列 | 注文ID |
|  `order_subtotal` (Overrides `_csubtotal`)  | 文字列 | 注文小計 |
|  `currency` (Overrides `_ccurrency`)  | 文字列 | 通貨 |
|  `order_coupon_code` (Overrides `_cpromo`)  | 文字列 | 割引コード |
|  `order_total` (Overrides `_ctotal`)  | 文字列 | 注文合計 |
|  `is_new_customer`  | ブール値 | 新規顧客か |
|  `product_unit_price`  | 数値の配列 | 商品単価 |
|  `quantity`  | 数値の配列 | 数量 |
|  `product_id`  | 配列 | 商品ID |
|  `product_name`  | 配列 | 商品名 |
|  `product_type`  | 配列 | 商品タイプ |
|  `product_vendor`  | 配列 | 商品ベンダー |
|  `variant_id`  | 配列 | バリアントID |
|  `variant_name`  | 配列 | バリアント名 |

### イベント

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
|  `alias` | エイリアス |
|  `lead` | リード |
|  `product` | 商品 |
|  `addtocart` | カートに追加 |
|  `checkout` | チェックアウト |
|  `purchase` | 購入 |

### イベント固有のパラメータ

イベントをマッピングするには、[イベントマッピングの作成](https://docs.tealium.com/manage-data-mappings/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `spotify_id` | Spotify Pixel ID  |
| `value` | 値 (`value`) |
| `discount_code` | 割引コード  |
| `category` | カテゴリー |
| `type` | タイプ | 
| `id` | ハッシュ化された内部ID  |
| `order_id` | 注文ID  |
| `order_subtotal` | 注文小計  | 
| `currency` | 通貨  |
| `order_coupon_code` |  割引コード  |
| `order_total` | 注文合計  |
| `is_new_customer` | 新規顧客か  |
| `product_unit_price` | 商品単価  |
| `quantity` | 数量  | 
| `product_id` | 商品ID |
| `product_name` | 商品名  |
| `product_type` | 商品タイプ  |
| `product_vendor` | 商品ベンダー  |
| `variant_id` | バリアントID | 
| `variant_name` |  バリアント名 |
| `alias` | エイリアス | 
| `lead` | リード | 
| `product` | 商品 | 
| `addtocart` | カートに追加 |
| `checkout` | チェックアウト |
| `purchase` | 購入 |
