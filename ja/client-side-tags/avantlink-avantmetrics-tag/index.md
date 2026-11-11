---
title: AvantLink AvantMetricsタグ構成ガイド
description: この記事では、タグ管理アカウントでAvantLink AvantMetricsタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/avantlink-avantmetrics-tag/
---
この記事では、AvantLink AvantMetricsタグを構成する方法について説明します。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[about-tags](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の構成を構成します。

* **サイトID**：マーチャントのサイトID。
 
## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `site_id` | 文字列 | サイトID。 |
| `new_customer` | ブール値 | 新規顧客かどうか。 |

### Eコマース

| 変数 | 型／値 | 説明 |
|:---------|:-----|:------------|
| `order_id` | 文字列 | 注文ID（`_corder`を上書き）。 |
| `amount` | 数値 | 注文の小計金額（`_csubtotal`を上書き）。 |
| `currency` | 文字列 | 通貨（`_ccurrency`を上書き）。 |
| `state` | 文字列 | 州（`_cstate`を上書き）。 |
| `country` | 文字列 | 国（`_ccountry`を上書き）。 |
| `ecc` | 文字列 | クーポンコード（`_cpromo`を上書き）。 |
| `tax` | 数値 | 課税額（`_ctax`を上書き）。 |
| `shipping` | 数値 | 配送料（`_cship`を上書き）。 |
| `parent_sku` | 配列 | 親SKU ID（`_cprod`を上書き）。 |
| `variant_sku` | 配列 | バリアントSKU ID（`_csku`を上書き）。 |
| `price` | 配列 | SKU価格（`_cprice`を上書き）。 |
| `qty` | 配列 | SKU数量（`_cquan`を上書き）。 |