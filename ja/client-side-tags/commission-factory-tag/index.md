---
title: Commission Factoryタグ構成ガイド
description: この記事では、Commission Factoryマーケットプレイタグを追加して構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/commission-factory-tag/
---
## 要件

* Commission Factoryタグには、[Eコマース拡張機能](https://docs.tealium.com/e-commerce-extension/)が必要です。
* 拡張機能を追加し、`_corder`、`_csubtotal`、`_csku`、`_cprice,`、`_cquan`変数を対応するデータソースにマッピングする必要があります。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の項目を構成します。

* **タグID**：Commission Factoryから提供される整数値。
* **CFオブジェクト名**：コマンドの実行に使用する変数。デフォルト値は**cf**です。

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。読み込みルールの詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

このタグのマッピングは、Eコマース拡張機能によって自動的に処理されます。

使用可能なカテゴリは次のとおりです。

### 標準

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `tag_id` | 文字列 | タグID |
| `namespace` | 文字列 | CFオブジェクト名 |

### Eコマース

| 変数 | タイプ | 説明 |
|:---------|:-----|:------------|
| `reference` | 文字列 | 参照1 |
| `reference2` | 文字列 | 参照2 |
| `reference3` | 文字列 | 参照3 |
| `reference4` | 文字列 | 参照4 |
| `customer_type` | 文字列 | 顧客タイプ |
| `order_id` | 文字列 | 注文ID（`_corder`を上書き） |
| `order_subtotal` | 文字列 | 小計／金額（`_csubtotal`を上書き） |
| `order_currency` | 文字列 | 通貨（`_ccurrency`を上書き） |
| `order_coupon_code` | 文字列 | プロモーションコード／クーポン（`_cpromo`を上書き） |
| `product_sku` | 配列 | SKUのリスト（`_csku`を上書き） |
| `product_quantity` | 配列 | 数量のリスト（`_cquan`を上書き） |
| `product_unit_price` | 配列 | 価格のリスト（`_cprice`を上書き） |