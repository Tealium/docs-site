---
title: Tealiumの構成
description: この記事では、Tealium Shopifyアプリをインストールする前に完了しておくべきTealiumの構成手順について説明します。
url: https://docs.tealium.com/ja/platforms/shopify/tealium-shopify-configuration/
---
Tealium ShopifyアプリからTealium iQタグ管理またはTealium EventStream APIハブにイベントデータを送信するには、以下が必要です：

* Tealium HTTP APIデータソース
* EventStreamとデータソースに送信するイベントのイベント仕様
* `restock`という名前のデータレイヤー変数

データソース、データソースイベント仕様、データレイヤー変数はTealiumアプリのインストール中に使用され、アプリをインストールする前に作成しておく必要があります。

## `restock`変数を作成する

`restock`という名前のブール型のデータレイヤー変数を作成します。データレイヤー変数の作成についての詳細は、[変数を追加する]()を参照してください。

## イベント仕様を作成する

イベント仕様の作成についての詳細は、[イベント仕様を管理する]()を参照してください。

### Shopify返金イベント仕様

`shopify_refund`イベント仕様を作成し、以下のユニバーサルデータオブジェクト属性をイベント仕様に追加します：

| 属性名 | データ型 |
|----|----|
| `customer_id` | 文字列 |
| `note` | 文字列 |
| `order_currency` | 文字列 |
| `order_discount` | 数値 |
| `order_id` | 文字列 |
| `order_tax` | 数値 |
| `order_total` | 数値 |
| `product_category` | 文字列の配列 |
| `product_id` | 文字列の配列 |
| `product_name` | 文字列の配列 |
| `product_quantity` | 数値の配列 |
| `product_sku` | 任意 |
| `product_unit_price` | 数値の配列 |
| `restock` | ブール型 |

### ショッピングカートイベント仕様

`cart_add`と`cart_remove`イベント仕様を作成し、以下のユニバーサルデータオブジェクト属性をイベント仕様に追加します：

| 属性名 | データ型 |
|-------------------------|--------------------|
| `cart_total_items` | 数値 |
| `cart_total_value` | 数値 |
| `customer_logged_in` | ブール型 |
| `language_code` | 文字列 |
| `page_name` | 文字列 |
| `page_type` | 文字列 |
| `product_brand` | 文字列の配列 |
| `product_category` | 文字列 |
| `product_currency` | 文字列 |
| `product_id` | 文字列の配列 |
| `product_image_url` | 文字列の配列 |
| `product_main_id` | 数値の配列 |
| `product_name` | 文字列の配列 |
| `product_normal_price` | 数値の配列 |
| `product_one_variant` | ブール型の配列 |
| `product_quantity` | 数値の配列 |
| `product_unit_price` | 数値の配列 |
| `product_url` | 文字列 |
| `tealium_visitor_id` | 文字列 |

### 購入イベント仕様

`purchase`イベント仕様を作成し、以下のユニバーサルデータオブジェクト属性をイベント仕様に追加します：

|属性名|データ型 |例の値|
|---|-----|----|
| `site_section`| 文字列 | &#34;order&#34; |
| `tealium_from_checkout`| 整数 | 1 |
| `customer_country`| 文字列| &#34;CA&#34; |
| `customer_state`| 文字列 | &#34;AB&#34; |
| `customer_city`| 文字列 | &#34;Calgary&#34; |
| `customer_zip`| 文字列 | &#34;T2J 6P4&#34; |
| `customer_id`| 文字列 | &#34;6691629760567&#34; |
| `customer_logged_in`| ブール型 | &#34;false&#34; |
| `customer_email`| 文字列 | &#34;user.name@example.com&#34;|
| `customer_first_name`| 文字列 | &#34;user&#34; |
| `customer_last_name`| 文字列 | &#34;name&#34; |
| `country_code`| 文字列 | &#34;CA&#34; |
| `order_id`| 文字列 | &#34;5853792796727&#34;|
| `order_subtotal`| 数値 | 2400 |
| `order_total`| 数値 | 2400 |
| `order_currency`| 文字列 | &#34;CAD&#34; |
| `order_tax`| 数値 | 0 |
| `order_shipping`| 数値 | 0 |
| `order_discount_amount` | 文字列 | &#34;&#34; |
| `payment_gateway`| 文字列 | &#34;shopify_payments&#34; |
| `product_id`| 文字列の配列 | [&#34;6933873000503&#34;] |
| `product_on_page`| 文字列の配列 | [&#34;6933873000503&#34;] |
| `product_quantity`| 数値の配列 | [4] |
| `product_unit_price`| 数値の配列 | [2400] |
| `product_name`| 文字列の配列 | [&#34;Dress Shirts&#34;] |
| `product_sku`| 数値の配列 | [&#34;40586935402551&#34;] |
| `page_name`| 文字列 | &#34;Information - Tealiumapp - Checkout&#34;|
| `cart_total_items`| 数値 | 1 |
| `cart_total_value`| 数値 | 2400 |
| `page_type`| 文字列 | &#34;order&#34; |
| `tealium_event` | 文字列 | &#34;purchase&#34; |
| `tealium_visitor_id` | 文字列 | &#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34; |

## HTTP APIデータソースを作成する

以下のイベント仕様を持つHTTP APIデータソースを作成します：

* `cart_add`
* `cart_remove`
* `checkout`
* `purchase`
* `shopify_refund`

データソースの作成についての詳細は、[データソースを作成する]()を参照してください。

変更を保存し、公開します。