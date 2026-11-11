---
title: United Internet Media（UIM）リターゲティングタグ構成ガイド
description: この記事では、United Internet Media（UIM）リターゲティングタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/uim-tag/
---
## タグに関するヒント

* マッピングを使用して、タグ構成を上書きまたは動的に構成します。
* マッピングを使用してイベントをトリガーします。
* 次のEコマース拡張パラメータをサポートしています。
    + 注文ID（`_corder`を上書き）
    + 注文商品（`_cprod`を上書き）
    + 注文合計（`_ctotal`を上書き）
    + 注文の送料（`_cship`を上書き）
    + 注文通貨（`_ccurrency`を上書き）
    + 商品ID（`_cprod`を上書き）
    + 商品名（`_cprodname`を上書き）
    + 商品価格（` _cprice`を上書き）
    + 商品通貨（`_ccurrency`を上書き）
    + バスケット合計（`_ctotal`を上書き）
    + バスケット内の商品（`_cprod`を上書き）
    + バスケット通貨（`_ccurrency`を上書き）

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際は、次の構成を行います。

* **広告主**：JS URL内の広告主。必須です。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは次のとおりです。

### 標準

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `advertiser` | 文字列 | 広告主 |
| `uuid_netid` | 文字列 | UUID netid |
| `privacy_law` | 文字列 | プライバシー法 |
| `privacy_consent` | 文字列 | プライバシー同意 |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `page_name` | 文字列 | ページ名 |
| `category_id` | 文字列 | カテゴリーID |
| `category_name` | 文字列 | カテゴリー名 |
| `product_id`（`_cprod`を上書き） | 文字列 | 商品ID |
| `product_name`（`_cprodname`を上書き） | 文字列 | 商品名 |
| `product_price`（`_cprice`を上書き） | 文字列 | 商品価格 |
| `product_currency`（`_ccurrency`を上書き） | 文字列 | 商品通貨 |
| `basket_total`（`_ctotal`を上書き） | 文字列 | バスケット合計 |
| `basket_items`（`_cprod`を上書き） | 文字列 | バスケット内の商品 |
| `basket_currency`（`_ccurrency`を上書き） | 文字列 | バスケット通貨 |
| `order_id`（`_corder`を上書き） | 文字列 | 注文ID |
| `order_items`（`_cprod`を上書き） | 文字列 | 注文商品 |
| `order_total`（`_ctotal`を上書き） | 文字列 | 注文合計 |
| `order_shipping`（`_cship`を上書き） | 文字列 | 注文の送料 |
| `order_currency`（`_ccurrency`を上書き） | 文字列 | 注文通貨 |

### イベントトリガー

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `general` | 一般 |
| `category` | カテゴリー |
| `product` | 商品 |
| `basket` | バスケット |
| `checkout` | チェックアウト |

### イベント固有のパラメータ

イベントをマッピングする方法については、[イベントマッピングの作成](https://docs.tealium.com/ja/tag-management/data-mappings/manage/#add-an-event-mapping)を参照してください。

| 変数 | 説明 |
|:---------|:------------|
| `general` | 一般 |
| `category` | カテゴリー |
| `product` | 商品 |
| `basket` | バスケット |
| `checkout` | チェックアウト |