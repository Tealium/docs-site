---
title: Kissmetricsタグ構成ガイド
description: この記事では、Kissmetricsタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/kissmetrics-tag/
---
Kissmetricsは、顧客獲得率と保持率を向上させ、より賢明なビジネス決定を行い、利益を増加させるための強力なウェブ分析ソリューションです。

## タグのヒント

* マッピングを使用して：
    * KM APIキーの標準構成値を上書きします
    * E-Commerce拡張値を上書きします
    * マップされたデータを含む` _kmq.push()`への呼び出しをトリガーします
* 注文IDが構成されていると、購入イベントは自動的に記録されます。すべてのE-Commerce拡張値がサポートされています。
* `_kmq.push`マッピングの例：
    * `[&#39;record&#39;, &#39;EVENT_NAME&#39;]`
    * `[&#39;record&#39;, &#39;EVENT_NAME&#39;, {&#39;PROPERTY_NAME&#39;:&#39;VALUE&#39;}]`
    * `[&#39;record&#39;, &#39;EVENT_NAME&#39;, {&#39;PROPERTY_NAME&#39;:&#39;VALUE&#39;}, CALLBACK_FUNCTION]`
    * `[&#39;set&#39;, {&#39;PROPERTY_NAME&#39;:&#39;VALUE&#39;}]`
    * `[&#39;identify&#39;, &#39;IDENTITY&#39;]`
* 共通メソッド：[Kissmetrics API Common Metrics](https://support.kissmetrics.io/docs/common-methods).

## タグ構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[About tags]()を参照してください。

タグを追加する際には、以下の構成を行います：

* **KM API Key**: KISSmetricsのURLに含まれる長い文字列と数字。例えば、`//doug1izaerwt3.cloudfront.net/YOUR_API_KEY.1.js`。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[About load rules]()を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数へデータを送信するプロセスです。詳細については、[About data mappings]()を参照してください。

利用可能なカテゴリーは以下の通りです：

### 標準

| 変数 | 説明 |
|:---------|:------------|
| `kmkey`  | APIキー |
| `kmq_push` | Kissmetricsキュー(`kmq`)にキューイングされたすべてのデータをプッシュする呼び出しをトリガーします。 |

### E-Commerce

| 変数 | タイプ | 説明 |
|:---------|:------------|:------------|
| `order_id` (`_corder`を上書き) |テキスト |注文ID  |
| `order_total` (`_ctotal`を上書き) | テキスト |注文合計  |
| `order_subtotal` (`_csubtotal`を上書き) | テキスト | 小計  | 
| `shipping_amt` (`_cship`を上書き) | テキスト |送料  |
| `tax_amt` (`_ctax`を上書き) | テキスト |税金  | 
| `store` (`_cstore`を上書き) | テキスト |ストア  | 
| `currency` (`_ccurrency`を上書き) | テキスト |通貨  |
| `promocode` (`_cpromo`を上書き) | テキスト |プロモーションコード  | 
| `cart_type` (`_ctype`を上書き) |テキスト |カートまたは注文タイプ  |
| `custid` (`_ccustid`を上書き) | テキスト |顧客ID  |
| `city` (`_ccity`を上書き) | テキスト |顧客の都市  | 
| `state` (`_cstate`を上書き) | テキスト |顧客の州  |
| `zip` (`_czip`を上書き) |  テキスト |顧客のZIPコード | 
| `country` (`_ccountry`を上書き) | テキスト | 顧客の国  |
| `product_ids` (`_cprod`を上書き)  | 配列 |  商品IDのリスト |
| `product_names` (`_cprodname`を上書き)  | 配列 | 名前のリスト |
| `product_skus` (`_csku`を上書き)  | 配列 | SKUのリスト |
| `product_brands` (`_cbrand`を上書き)  | 配列 | ブランドのリスト |
| `product_categories` (`_ccat`を上書き)  | 配列 | カテゴリーのリスト |
| `product_categories2` (`_ccat2`を上書き)  | 配列 | カテゴリー2のリスト |
| `product_quantities` (`_cquan`を上書き)  | 配列 | 数量のリスト |
| `product_prices` (`_cprice`を上書き)  | 配列 | 価格のリスト |
| `product_discounts` (`_cpdisc`を上書き)  | 配列 | 割引のリスト |

