---
title: Kissmetricsタグ構成ガイド
description: この記事では、Kissmetricsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kissmetrics-tag/
---
Kissmetricsは、顧客獲得率と顧客維持率の向上、より的確なビジネス上の意思決定、収益の改善を支援する強力なWeb分析ソリューションです。

## タグに関するヒント

* マッピングを使用して、以下を行います。
    * KM APIキーの標準構成値を上書きする
    * Eコマース拡張機能の値を上書きする
    * マッピングされたデータを含む` _kmq.push()`の呼び出しをトリガーする
* 注文IDが構成されると、購入イベントが自動的に記録されます。Eコマース拡張機能のすべての値がサポートされています。
* `_kmq.push`のマッピング例：
    * `['record', 'EVENT_NAME']`
    * `['record', 'EVENT_NAME', {'PROPERTY_NAME':'VALUE'}]`
    * `['record', 'EVENT_NAME', {'PROPERTY_NAME':'VALUE'}, CALLBACK_FUNCTION]`
    * `['set', {'PROPERTY_NAME':'VALUE'}]`
    * `['identify', 'IDENTITY']`
* 一般的なメソッド：[Kissmetrics APIの一般的なメトリクス](https://support.kissmetrics.io/docs/common-methods)。

## タグの構成

タグマーケットプレイスに移動して、新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加する際に、以下の項目を構成します。

* **KM APIキー**：KISSmetricsのURLに含まれる、英字と数字で構成された長い文字列です。例：`//doug1izaerwt3.cloudfront.net/YOUR_API_KEY.1.js`

## 読み込みルール

すべてのページでタグを読み込むか、タグを読み込む条件を構成します。詳細については、[読み込みルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

データマッピングは、データレイヤー変数の値をベンダータグ内の対応する変数に送信します。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

使用可能なカテゴリーは以下のとおりです。

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `kmkey`  | APIキー |
| `kmq_push` | Kissmetricsキュー（`kmq`）にキューイングされているすべてのデータをプッシュする呼び出しをトリガーします。 |

### Eコマース

| 変数 | 型 | 説明 |
|:---------|:------------|:------------|
| `order_id`（`_corder`を上書き） | テキスト | 注文ID |
| `order_total`（`_ctotal`を上書き） | テキスト | 注文合計 |
| `order_subtotal`（`_csubtotal`を上書き） | テキスト | 小計 |
| `shipping_amt`（`_cship`を上書き） | テキスト | 配送料 |
| `tax_amt`（`_ctax`を上書き） | テキスト | 税額 |
| `store`（`_cstore`を上書き） | テキスト | ストア |
| `currency`（`_ccurrency`を上書き） | テキスト | 通貨 |
| `promocode`（`_cpromo`を上書き） | テキスト | プロモーションコード |
| `cart_type`（`_ctype`を上書き） | テキスト | カートまたは注文のタイプ |
| `custid`（`_ccustid`を上書き） | テキスト | 顧客ID |
| `city`（`_ccity`を上書き） | テキスト | 顧客の市区町村 |
| `state`（`_cstate`を上書き） | テキスト | 顧客の州 |
| `zip`（`_czip`を上書き） | テキスト | 顧客の郵便番号 |
| `country`（`_ccountry`を上書き） | テキスト | 顧客の国 |
| `product_ids`（`_cprod`を上書き） | 配列 | 商品IDのリスト |
| `product_names`（`_cprodname`を上書き） | 配列 | 名前のリスト |
| `product_skus`（`_csku`を上書き） | 配列 | SKUのリスト |
| `product_brands`（`_cbrand`を上書き） | 配列 | ブランドのリスト |
| `product_categories`（`_ccat`を上書き） | 配列 | カテゴリーのリスト |
| `product_categories2`（`_ccat2`を上書き） | 配列 | カテゴリー2のリスト |
| `product_quantities`（`_cquan`を上書き） | 配列 | 数量のリスト |
| `product_prices`（`_cprice`を上書き） | 配列 | 価格のリスト |
| `product_discounts`（`_cpdisc`を上書き） | 配列 | 割引のリスト |