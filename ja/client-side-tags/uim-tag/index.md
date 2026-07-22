---
title: ユナイテッドインターネットメディア（UIM）リターゲティングタグ構成ガイド
description: この記事では、ユナイテッドインターネットメディア（UIM）のリターゲティングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/uim-tag/
---
## タグのヒント

* マッピングを使用してタグの構成を上書きしたり、動的に構成します。
* マッピングを使用してイベントをトリガーします。
* 以下のE-Commerce拡張パラメータをサポートしています：
    + 注文ID（`_corder`を上書き）
    + 注文アイテム（`_cprod`を上書き）
    + 注文合計（`_ctotal`を上書き）
    + 注文の配送（`_cship`を上書き）
    + 注文通貨（`_ccurrency`を上書き）
    + 商品ID（`_cprod`を上書き）
    + 商品名（`_cprodname`を上書き）
    + 商品価格（`_cprice`を上書き）
    + 商品通貨（`_ccurrency`を上書き）
    + バスケット合計（`_ctotal`を上書き）
    + バスケットアイテム（`_cprod`を上書き）
    + バスケット通貨（`_ccurrency`を上書き）



## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際には、以下の構成を行います：

* **広告主**：JS URLの広告主。必須

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリは以下の通りです：

### スタンダード

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
|  `advertiser`  | String | 広告主 | 
|  `uuid_netid`  | String | UUID netid |
|  `privacy_law`  | String | プライバシー法 |
|  `privacy_consent`  | String | プライバシー同意|

### E-Commerce

| 変数 | タイプ |説明 |
|:---------|:------------|:------------|
|  `page_name`  | String | ページ名 |
|  `category_id`  | String | カテゴリID |
|  `category_name`  | String | カテゴリ名 |
|  `product_id` (Overrides `_cprod`)  | String | 商品ID |
|  `product_name` (Overrides `_cprodname`)  | String | 商品名 |
|  `product_price` (Overrides `_cprice`)  | String | 商品価格 |
|  `product_currency` (Overrides `_ccurrency`)  | String | 商品通貨 |
|  `basket_total` (Overrides `_ctotal`)  | String | バスケット合計 |
|  `basket_items` (Overrides `_cprod`)  | String | バスケットアイテム |
|  `basket_currency` (Overrides `_ccurrency`)  | String | バスケット通貨 |
|  `order_id` (Overrides `_corder`)  | String | 注文ID |
|  `order_items` (Overrides `_cprod`)  | String | 注文アイテム |
|  `order_total` (Overrides `_ctotal`)  | String | 注文合計 |
|  `order_shipping` (Overrides `_cship`)  | String | 注文の配送 |
|  `order_currency` (Overrides `_ccurrency`)  | String | 注文通貨 |

### イベントトリガー
イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `general` | 一般 |
| `category` | カテゴリ |
| `product` | 商品 |
| `basket` | バスケット |
| `checkout` | チェックアウト |

### イベント固有のパラメータ
イベントをマップするには、[イベントマッピングの作成](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `general` | 一般 |
| `category` | カテゴリ|
| `product` | 商品 |
| `basket` | バスケット |
| `checkout` | チェックアウト |

