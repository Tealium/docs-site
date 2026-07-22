---
title: Wunderkindタグ構成ガイド
description: この記事では、Tealium iQタグ管理アカウントでWunderkindタグを構成する方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/wunderkind-tag/
---
## タグのヒント

マッピングを使用して：

* `website_id`を動的に上書きします。
* 下記のE-Commerce拡張値を動的に上書きします。
* 他の必須およびオプションのパラメーターの値を構成します。

変換イベントをトリガーするための必須パラメーター：

* 注文ID
* 顧客ID/メール
* 目標
* 通貨
* 税金額
* 送料
* 小計/金額
* 商品SKU

このタグは以下のE-Commerce拡張値をサポートしています：

* 注文ID（`order_id`に行きます）
* 注文小計（`amount`に行きます）
* 顧客ID（`email`に行きます）
* 通貨
* プロモーションコード（`coupon`に行きます）
* 商品/アイテムID
* 商品/アイテムSKU
* 商品/アイテムの数量
* 商品/アイテムの価格
* 税金額
* 送料

E-Commerce拡張を使用しており、上記の値を使用するように構成している場合、これらのパラメーターのマッピングを構成する必要はありません。

## タグの構成

タグマーケットプレイスに移動して新しいタグを追加します。詳細については、[タグについて](https://docs.tealium.com/about-tags/)を参照してください。

タグを追加するときに、以下の構成を行います：

* **ウェブサイトID**：あなたのWunderkindウェブサイトID。クライアントIDとも呼ばれます。

## ロードルール

すべてのページでタグをロードするか、タグがロードされる条件を構成します。詳細については、[ロードルールについて](https://docs.tealium.com/about-load-rules/)を参照してください。

## データマッピング

マッピングは、データレイヤー変数からベンダータグの対応する宛先変数にデータを送信するプロセスです。詳細については、[データマッピングについて](https://docs.tealium.com/about-data-mappings/)を参照してください。

利用可能なカテゴリーは以下の通りです：

### スタンダード

| **変数** | **説明** |
|:---------|:------------|
| `website_id` | ウェブサイトID |
| `phone` | 電話 |
| `goal` | 目標 |
| `transaction_origin` | 取引元 |
| `total_discount` | 合計割引 |
| `pay_method` | 支払い方法 |

### E-Commerce

| **変数** | **説明** | **データタイプ** |
|:---------|:------------|:------------|
| `order_id` | 注文ID（`_corder`を上書き） | 文字列 |
| `customer_id` | 顧客ID（`_ccustid`を上書き） | 文字列 |
| `order_subtotal` | 小計（`_csubtotal`を上書き） | 整数 |
| `order_currency` | 通貨（`_ccurrency`を上書き） | 文字列 |
| `promo_code` | プロモーションコード（`_cpromo`を上書き） | 文字列 |
| `product_id` | 商品IDのリスト（`_cprod`を上書き） | 配列 |
| `product_sku` | SKUのリスト（`_csku`を上書き） | 配列 |
| `product_quantity` | 数量のリスト（`_cquan`を上書き） | 配列 |
| `product_unit_price` | 価格のリスト（`_cprice`を上書き） | 配列 |
| `order_tax` | 税金額（`_ctax`を上書き） | 配列 |
| `shipping_amount` | 送料（`_cship`を上書き） | 配列 |

