---
title: Partnerizeイベントトラッカータグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでPartnerizeイベントトラッカータグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/partnerize-event-tracker-tag/
---
## タグのヒント

* Order CurrencyはデフォルトでE-Commerce拡張の値になります。
* このタグは以下のE-Commerce拡張パラメータを使用します：
    * Order ID
    * Order Currency
    * Order Promo Code
    * SKUのリスト
    * カテゴリのリスト
    * 数量のリスト
    * 価格のリスト
* カスタム製品パラメータのマッピングは配列であるべきです。
* カスタムコンバージョンパラメータのマッピングは文字列であるべきです。

## タグの構成

新しいタグを追加するためにタグマーケットプレイスに移動します。タグの追加方法については、[Tag Overview](https://docs.tealium.com/about-tags/)の記事を参照してください。

タグを追加する際には、以下の構成を行います：

* **Campaign**: デフォルトのキャンペーン。
* **Adref**: Partnerizeが提供する値。
* **Customer Type**: デフォルトの顧客タイプ。
* **Country**: 訪問または販売地点の国の2文字のISOコード。
* **Default Currency**: コンバージョンが発生する通貨の3文字のISOコード。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。ロードルールについての詳細は、[Load Rules](https://docs.tealium.com/about-load-rules/)のドキュメンテーションを参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。変数をタグの宛先にマップする方法については、[data mappings](https://docs.tealium.com/ja/iq-tag-management/data-mappings/manage/)を参照してください。

利用可能なカテゴリは以下の通りです：

### 標準

| 変数 | 説明 |
| --- | --- |
| Campaign | (campaign) |
| Customertype | (customertype) |
| Custref/Customer ID | (customer_id) |
| Country | (country) |
| Adref | (adref) |
| Custom Conversion Parameter | (conversion.###) |
| Custom Product Parameter | (product.###) |

### E-Commerce

| 変数 | 説明 |
| --- | --- |
| Conversionref/Order ID | (order_id) (_corderを上書き) |
| Currency | (currency) (_ccurrencyを上書き) |
| Voucher/Promo Code | (voucher) (_cpromoを上書き) |
| SKUのリスト (product_sku) (_cskuを上書き) | [配列] |
| カテゴリのリスト (product_category) (_ccatを上書き) | [配列] |
| 数量のリスト (product_quantity) (_cquanを上書き) | [配列] |
| 価格のリスト (product_unit_price) (_cpriceを上書き) | [配列] |

