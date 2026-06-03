---
title: データレイヤーとイベント
description: この記事では、Tealium Shopifyアプリによって追跡されるデータレイヤー変数とイベントについての情報を提供します。
url: https://docs.tealium.com/ja/platforms/shopify/data-layer-and-events/
---
Tealiumのデータレイヤーとユニバーサルデータオブジェクトについての詳細は、[データレイヤー入門]()および[ユニバーサルデータオブジェクト]()をご覧ください。

## サポートされる変数

以下のユニバーサルデータレイヤー変数がTealium Shopifyアプリでサポートされています：

|変数|説明|
|---|---|
|`cart_total_items`|整数|
|`cart_total_value`|浮動小数点|
|`country_code`|文字列|
|`customer_city`|文字列|
|`customer_country`|文字列|
|`customer_email`|文字列|
|`customer_first_name`|文字列|
|`customer_id`|文字列|
|`customer_last_name`|文字列|
|`customer_logged_in`|ブール値|
|`customer_state`|文字列|
|`customer_zip`|文字列|
|`language_code`|文字列|
|`order_currency`|文字列|
|`order_discount_amount`|文字列|
|`order_id`|文字列|
|`order_shipping`|浮動小数点|
|`order_subtotal`|浮動小数点|
|`order_tax`|浮動小数点|
|`order_total`|浮動小数点|
|`page_name`|文字列|
|`page_type`|文字列|
|`payment_gateway`|文字列|
|`product_brand`|リスト|
|`product_category`|リスト|
|`product_currency`|文字列|
|`product_id`|リスト|
|`product_image_url`|リスト|
|`product_main_id`|リスト|
|`product_name`|リスト|
|`product_normal_price`|リスト|
|`product_on_page`|リスト|
|`product_one_variant`|リスト|
|`product_price`|リスト|
|`product_quantity`|リスト|
|`product_sku`|リスト|
|`product_unit_price`|リスト|
|`product_url`|リスト|
|`search_keyword`|文字列|
|`search_results`|整数|
|`site_section`|文字列|
|`tealium_event`|文字列|
|`tealium_from_checkout`|整数|
|`tealium_visitor_id`|文字列|

## クライアント側の例示データ

以下のセクションでは、特定のイベントの例示データを示します。

### page_viewおよびcategory_viewイベントの例示データ

|変数|例示値|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`page_name`|&#34;女性服&#34;|
|`page_type`|&#34;page&#34;|
|`product_on_page`|[&#34;40586935271479&#34;, &#34;40586935664695&#34;, &#34;40586935599159&#34;, &#34;40586935402551&#34;, &#34;40586935762999&#34;,…]|
|`site_section`|&#34;collection&#34;|
|`tealium_event`|&#34;page_view&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

### product_viewイベントの例示データ

|変数|例示値 |
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`page_name`|&#34;女性靴&#34;|
|`page_type`|&#34;product&#34;|
|`product_brand`|[&#34;XYZ Shoes&#34;]|
|`product_id`|[&#34;6933873000503&#34;]|
|`product_name`|[&#34;フラットシューズ&#34;]|
|`product_price`|[&#34;600.00&#34;]|
|`product_sku`|[&#34;&#34;]|
|`site_section`|&#34;product&#34;|
|`tealium_event`|&#34;product_view&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

#### cart_add / cart_removeイベントの例示データ

|変数|例示値|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`page_name`|&#34;女性服&#34;|
|`page_type`|&#34;product&#34;|
|`product_brand`|[&#34;XYZ Clothing&#34;]|
|`product_category`|[&#34;&#34;]|
|`product_currency`|&#34;CAD&#34;|
|`product_id`|[&#34;40586935402551&#34;]|
|`product_image_url`|[&#34;&#34;]|
|`product_main_id`|[6933873000503]|
|`product_name`|[&#34;XYZ Womens&#39;s Flats&#34;]|
|`product_normal_price`|[600]|
|`product_one_variant`|[true]|
|`product_quantity`|[1]|
|`product_unit_price`|[600]|
|`product_url`|[&#34;/products/the-collection-snowboard-hydrogen?variant=40586935402551&#34;]|
|`tealium_event`|&#34;cart_add&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

### searchイベントの例示データ

|変数|例示値|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`search_keyword`|&#34;靴&#34;|
|`search_results`|12|
|`site_section`|&#34;search&#34;|
|`page_name`|&#34;検索: 「靴」に対する12件の結果が見つかりました&#34;|
|`product_on_page`|[&#34;40586935009335&#34;, &#34;40586935566391&#34;, &#34;40586935500855&#34;, &#34;40586934976567&#34;, &#34;40586935402551&#34;,…]|
|`tealium_event`|&#34;search&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

### checkoutイベントの例示データ

|変数|例示値|
|---|---|
| `site_section` | &#34;order&#34; |
| `tealium_from_checkout` | 1 |
| `page_name` | &#34;チェックアウト：開始&#34; |
| `page_type` | &#34;checkout&#34; |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | &#34;checkout&#34; |
| `tealium_visitor_id` | &#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34; |

### checkout_address_info_submittedイベントの例示データ

|変数|例示値|
|---|---|
| `site_section` | &#34;order&#34; |
| `tealium_from_checkout` | 1 |
| `page_name` | &#34;チェックアウト：フォーム&#34; |
| `page_type` | &#34;checkout&#34; |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | &#34;checkout_address_info_submitted&#34; |
| `tealium_visitor_id` | &#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34; |

### purchaseイベントの例示データ

|変数|例示値|
|---|---|
|`site_section`|&#34;order&#34;|
|`tealium_from_checkout`|1|
|`customer_country`|&#34;US&#34;|
|`customer_state`|&#34;CA&#34;|
|`customer_city`|&#34;San Diego&#34;|
|`customer_zip`|&#34;92121&#34;|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_logged_in`|&#34;false&#34;|
|`customer_email`|&#34;user.name@example.com&#34;|
|`customer_first_name`|&#34;user&#34;|
|`customer_last_name`|&#34;name&#34;|
|`country_code`|&#34;US&#34;|
|`order_id`|&#34;5853792796727&#34;|
|`order_subtotal`|2400|
|`order_total`|2400|
|`order_currency`|&#34;USD&#34;|
|`order_tax`|0|
|`order_shipping`|0|
|`order_discount_amount`|&#34;&#34;|
|`payment_gateway`|&#34;shopify_payments&#34;|
|`product_id`|[&#34;6933873000503&#34;]|
|`product_on_page`|[&#34;6933873000503&#34;]|
|`product_quantity`|[4]|
|`product_unit_price`|[2400]|
|`product_name`|[&#34;XYZ Women&#39;s Flats&#34;]|
|`product_sku`|[&#34;40586935402551&#34;]|
|`page_name`|&#34;情報 - Tealiumapp - チェックアウト&#34;|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`page_type`|&#34;order&#34;|
|`tealium_event`|&#34;purchase&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

## Webhook例示データ

以下のセクションでは、特定のイベントの例示データを示します。

### ORDERS_CREATEイベントの例示データ

#### 注文識別子

|変数|例示値|
|---|---|
| `order_id` |  &#34;5853792796727&#34; |
| `order_name` | &#34;注文 #12345&#34; |
| `order_number` | &#34;12345&#34; |
| `checkout_token` | &#34;abcdef123456&#34; |
| `confirmation_number` | &#34;CONF123456&#34; |
| `landing_site` | &#34;/landing-page&#34; |
| `order_created_at` | &#34;2024-06-01T12:34:56Z&#34; |

#### 注文財務情報

|変数|例示値|
|---|---|
|`order_total`|2400|
|`order_subtotal`|2400|
| `order_discount` | 0 |
| `order_tax` | 0 |
| `order_shipping` | 0 |
| `order_currency` | &#34;USD&#34; |
| `order_payment_type` | &#34;VISA&#34;|
| `order_coupon_code` | &#34;20SAVE&#34; |
| `order_shipping_type` | &#34;Fedex&#34; |

#### 顧客データ

|変数|例示値|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_email`|&#34;user.name@example.com&#34;|
| `customer_first_name` | &#34;John&#34; |
| `customer_last_name` | &#34;Smith&#34; |
| `customer_city` | &#34;San Diego&#34; |
| `customer_country` | &#34;US&#34; |
| `customer_state` | &#34;CA&#34; |
| `customer_zip` | &#34;92121&#34; |
| `customer_email_marketing_consent` | &#34;True&#34; |
| `customer_sms_marketing_consent` | &#34;True&#34; |

#### 製品データ（行アイテムごとに1エントリ）

|変数|例示値|
|---|---|
| `product_id` | [&#34;6933873000503&#34;] |
| `product_variant` | [&#34;Size 8 / Black&#34;] |
| `product_name` | [&#34;XYZ Women&#39;s Flats&#34;] |
| `product_quantity` | [4] |
| `product_unit_price` | [2400] |
| `product_brand` | [&#34;XYZ&#34;] |
| `product_sku` | [&#34;40586935402551&#34;] |
| `product_category` | [&#34;Women&#39;s Shoes&#34;] |
| `product_discount` | [0] |
| `product_promo_code` | [&#34;20SAVE&#34;] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;purchase&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;orders/create&#34; |
### CHECKOUTS_CREATEの例示データ

|変数|例示値|
|---|---|
| `order_id` |  &#34;5853792796727&#34; |
| `checkout_token` | &#34;abcdef123456&#34; |
| `order_total` | 2400 |
| `order_subtotal` | 2400 |
| `order_discount` | 0 |
| `order_currency` | &#34;USD&#34; |

#### 商品データ（配列）

|変数|例示値|
|---|---|
| `product_id` | [&#34;6933873000503&#34;] |
| `product_variant` | [&#34;Size 8 / Black&#34;] |
| `product_name` | [&#34;XYZ Women&#39;s Flats&#34;] |
| `product_quantity` | [4] |
| `product_sku` | [&#34;40586935402551&#34;] |
| `product_category` | [&#34;Women&#39;s Shoes&#34;] |
| `product_discount` | [0] |
| `product_list_price` | [2400] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;checkouts_create&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;checkouts/create&#34; |

### REFUNDS_CREATEの例示データ

|変数|例示値|
|---|---|
| `order_id` |  &#34;5853792796727&#34; |
|`customer_id`|&#34;6691629760567&#34;|
| `order_currency` | &#34;USD&#34; |
|`order_total`|2400|
| `order_tax` | 0 |
| `order_discount` | 0 |
| `restock` | true |
| `note` | 文字列（返金理由） |

#### 返金された商品（配列）

|変数|例示値|
|---|---|
| `product_id` | [&#34;6933873000503&#34;] |
| `product_variant` | [&#34;Size 8 / Black&#34;] |
| `product_sku` | [&#34;40586935402551&#34;] |
| `product_quantity` | [2] |
| `product_name` | [&#34;XYZ Women&#39;s Flats&#34;] |
| `product_unit_price` | [2400] |
| `product_category` | [&#34;Women&#39;s Shoes&#34;] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;shopify_refund&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;refunds/create&#34; |

### CARTS_CREATE / CARTS_UPDATEの例示データ

|変数|例示値|
|---|---|
| `cart_token` | &#34;abcdef123456&#34; |
| `cart_total_items` | 2 |
| `cart_total_value` | 1200 |

#### 商品データ（配列）

|変数|例示値|
|---|---|
| `product_id` | [&#34;6933873000503&#34;] |
| `product_variant` | [&#34;Size 8 / Black&#34;] |
| `product_name` | [&#34;XYZ Women&#39;s Flats&#34;] |
| `product_quantity` | [2] |
| `product_unit_price` | [1200] |
| `product_brand` | [&#34;XYZ&#34;] |
| `product_category` | [&#34;Women&#39;s Shoes&#34;] |
| `product_discount` | [0] |
| `product_image_url` | [&#34;https://cdn.shopify.com/s/files/1/0000/0001/products/flats.jpg&#34;] |
| `product_url` | [&#34;/products/xyz-womens-flats?variant=6933873000503&#34;] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;cart_create&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;carts/create&#34; |

### CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATEの例示データ

|変数|例示値|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_email`| &#34;user.name@example.com&#34;|
| `consent_state` | &#34;subscribed&#34;  |
| `opt_in_level` | &#34;single_opt_in&#34;  |
| `consent_timestamp` | &#34;2024-06-01T12:34:56Z&#34; |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;email_consent_change&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;customers_email_marketing_consent/update&#34; |

### CUSTOMERS_MARKETING_CONSENT_UPDATE (SMS)の例示データ

|変数|例示値|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
| `consent_state` | &#34;subscribed&#34;|
| `opt_in_level` |&#34;single_opt_in&#34; |
| `consent_collected_from` | &#34;website&#34; |
| `consent_timestamp` | &#34;2024-06-01T12:34:56Z&#34; |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;sms_consent_change&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;customers_marketing_consent/update&#34; |

### CUSTOMERS_CREATEの例示データ

|変数|例示値|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_email`|&#34;user.name@example.com&#34;|
| `customer_first_name` | &#34;John&#34; |
| `customer_last_name` | &#34;Smith&#34; |
| `customer_city` | &#34;San Diego&#34; |
| `customer_country` | &#34;US&#34; |
| `customer_country_code` | &#34;US&#34; |
| `province` | &#34;California&#34; |
| `province_code` | &#34;CA&#34; |
| `order_currency` | &#34;USD&#34; |
| `shopify_tags` | &#34;wholesale,newsletter&#34; |
| `created_at` | &#34;2024-06-01T12:34:56Z&#34; |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | &#34;Shopify New Customer&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;customers/create&#34; |