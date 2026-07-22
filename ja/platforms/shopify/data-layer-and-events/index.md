---
title: データレイヤーとイベント
description: この記事では、Tealium Shopifyアプリによって追跡されるデータレイヤー変数とイベントについての情報を提供します。
url: https://docs.tealium.com/ja/platforms/shopify/data-layer-and-events/
---
Tealiumのデータレイヤーとユニバーサルデータオブジェクトについての詳細は、[データレイヤー入門](https://docs.tealium.com/an-introduction-to-the-data-layer/)および[ユニバーサルデータオブジェクト](https://docs.tealium.com/universal-data-object/)をご覧ください。

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
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`page_name`|"女性服"|
|`page_type`|"page"|
|`product_on_page`|["40586935271479", "40586935664695", "40586935599159", "40586935402551", "40586935762999",…]|
|`site_section`|"collection"|
|`tealium_event`|"page_view"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

### product_viewイベントの例示データ

|変数|例示値 |
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`page_name`|"女性靴"|
|`page_type`|"product"|
|`product_brand`|["XYZ Shoes"]|
|`product_id`|["6933873000503"]|
|`product_name`|["フラットシューズ"]|
|`product_price`|["600.00"]|
|`product_sku`|[""]|
|`site_section`|"product"|
|`tealium_event`|"product_view"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

#### cart_add / cart_removeイベントの例示データ

|変数|例示値|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`page_name`|"女性服"|
|`page_type`|"product"|
|`product_brand`|["XYZ Clothing"]|
|`product_category`|[""]|
|`product_currency`|"CAD"|
|`product_id`|["40586935402551"]|
|`product_image_url`|[""]|
|`product_main_id`|[6933873000503]|
|`product_name`|["XYZ Womens's Flats"]|
|`product_normal_price`|[600]|
|`product_one_variant`|[true]|
|`product_quantity`|[1]|
|`product_unit_price`|[600]|
|`product_url`|["/products/the-collection-snowboard-hydrogen?variant=40586935402551"]|
|`tealium_event`|"cart_add"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

### searchイベントの例示データ

|変数|例示値|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`search_keyword`|"靴"|
|`search_results`|12|
|`site_section`|"search"|
|`page_name`|"検索: 「靴」に対する12件の結果が見つかりました"|
|`product_on_page`|["40586935009335", "40586935566391", "40586935500855", "40586934976567", "40586935402551",…]|
|`tealium_event`|"search"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

### checkoutイベントの例示データ

|変数|例示値|
|---|---|
| `site_section` | "order" |
| `tealium_from_checkout` | 1 |
| `page_name` | "チェックアウト：開始" |
| `page_type` | "checkout" |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | "checkout" |
| `tealium_visitor_id` | "01902bf47c7200111b70236f67ee0506f004b06700fbe" |

### checkout_address_info_submittedイベントの例示データ

|変数|例示値|
|---|---|
| `site_section` | "order" |
| `tealium_from_checkout` | 1 |
| `page_name` | "チェックアウト：フォーム" |
| `page_type` | "checkout" |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | "checkout_address_info_submitted" |
| `tealium_visitor_id` | "01902bf47c7200111b70236f67ee0506f004b06700fbe" |

### purchaseイベントの例示データ

|変数|例示値|
|---|---|
|`site_section`|"order"|
|`tealium_from_checkout`|1|
|`customer_country`|"US"|
|`customer_state`|"CA"|
|`customer_city`|"San Diego"|
|`customer_zip`|"92121"|
|`customer_id`|"6691629760567"|
|`customer_logged_in`|"false"|
|`customer_email`|"user.name@example.com"|
|`customer_first_name`|"user"|
|`customer_last_name`|"name"|
|`country_code`|"US"|
|`order_id`|"5853792796727"|
|`order_subtotal`|2400|
|`order_total`|2400|
|`order_currency`|"USD"|
|`order_tax`|0|
|`order_shipping`|0|
|`order_discount_amount`|""|
|`payment_gateway`|"shopify_payments"|
|`product_id`|["6933873000503"]|
|`product_on_page`|["6933873000503"]|
|`product_quantity`|[4]|
|`product_unit_price`|[2400]|
|`product_name`|["XYZ Women's Flats"]|
|`product_sku`|["40586935402551"]|
|`page_name`|"情報 - Tealiumapp - チェックアウト"|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`page_type`|"order"|
|`tealium_event`|"purchase"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

## Webhook例示データ

以下のセクションでは、特定のイベントの例示データを示します。

### ORDERS_CREATEイベントの例示データ

#### 注文識別子

|変数|例示値|
|---|---|
| `order_id` |  "5853792796727" |
| `order_name` | "注文 #12345" |
| `order_number` | "12345" |
| `checkout_token` | "abcdef123456" |
| `confirmation_number` | "CONF123456" |
| `landing_site` | "/landing-page" |
| `order_created_at` | "2024-06-01T12:34:56Z" |

#### 注文財務情報

|変数|例示値|
|---|---|
|`order_total`|2400|
|`order_subtotal`|2400|
| `order_discount` | 0 |
| `order_tax` | 0 |
| `order_shipping` | 0 |
| `order_currency` | "USD" |
| `order_payment_type` | "VISA"|
| `order_coupon_code` | "20SAVE" |
| `order_shipping_type` | "Fedex" |

#### 顧客データ

|変数|例示値|
|---|---|
|`customer_id`|"6691629760567"|
|`customer_email`|"user.name@example.com"|
| `customer_first_name` | "John" |
| `customer_last_name` | "Smith" |
| `customer_city` | "San Diego" |
| `customer_country` | "US" |
| `customer_state` | "CA" |
| `customer_zip` | "92121" |
| `customer_email_marketing_consent` | "True" |
| `customer_sms_marketing_consent` | "True" |

#### 製品データ（行アイテムごとに1エントリ）

|変数|例示値|
|---|---|
| `product_id` | ["6933873000503"] |
| `product_variant` | ["Size 8 / Black"] |
| `product_name` | ["XYZ Women's Flats"] |
| `product_quantity` | [4] |
| `product_unit_price` | [2400] |
| `product_brand` | ["XYZ"] |
| `product_sku` | ["40586935402551"] |
| `product_category` | ["Women's Shoes"] |
| `product_discount` | [0] |
| `product_promo_code` | ["20SAVE"] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "purchase" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "orders/create" |
### CHECKOUTS_CREATEの例示データ

|変数|例示値|
|---|---|
| `order_id` |  "5853792796727" |
| `checkout_token` | "abcdef123456" |
| `order_total` | 2400 |
| `order_subtotal` | 2400 |
| `order_discount` | 0 |
| `order_currency` | "USD" |

#### 商品データ（配列）

|変数|例示値|
|---|---|
| `product_id` | ["6933873000503"] |
| `product_variant` | ["Size 8 / Black"] |
| `product_name` | ["XYZ Women's Flats"] |
| `product_quantity` | [4] |
| `product_sku` | ["40586935402551"] |
| `product_category` | ["Women's Shoes"] |
| `product_discount` | [0] |
| `product_list_price` | [2400] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "checkouts_create" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "checkouts/create" |

### REFUNDS_CREATEの例示データ

|変数|例示値|
|---|---|
| `order_id` |  "5853792796727" |
|`customer_id`|"6691629760567"|
| `order_currency` | "USD" |
|`order_total`|2400|
| `order_tax` | 0 |
| `order_discount` | 0 |
| `restock` | true |
| `note` | 文字列（返金理由） |

#### 返金された商品（配列）

|変数|例示値|
|---|---|
| `product_id` | ["6933873000503"] |
| `product_variant` | ["Size 8 / Black"] |
| `product_sku` | ["40586935402551"] |
| `product_quantity` | [2] |
| `product_name` | ["XYZ Women's Flats"] |
| `product_unit_price` | [2400] |
| `product_category` | ["Women's Shoes"] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "shopify_refund" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "refunds/create" |

### CARTS_CREATE / CARTS_UPDATEの例示データ

|変数|例示値|
|---|---|
| `cart_token` | "abcdef123456" |
| `cart_total_items` | 2 |
| `cart_total_value` | 1200 |

#### 商品データ（配列）

|変数|例示値|
|---|---|
| `product_id` | ["6933873000503"] |
| `product_variant` | ["Size 8 / Black"] |
| `product_name` | ["XYZ Women's Flats"] |
| `product_quantity` | [2] |
| `product_unit_price` | [1200] |
| `product_brand` | ["XYZ"] |
| `product_category` | ["Women's Shoes"] |
| `product_discount` | [0] |
| `product_image_url` | ["https://cdn.shopify.com/s/files/1/0000/0001/products/flats.jpg"] |
| `product_url` | ["/products/xyz-womens-flats?variant=6933873000503"] |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "cart_create" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "carts/create" |

### CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATEの例示データ

|変数|例示値|
|---|---|
|`customer_id`|"6691629760567"|
|`customer_email`| "user.name@example.com"|
| `consent_state` | "subscribed"  |
| `opt_in_level` | "single_opt_in"  |
| `consent_timestamp` | "2024-06-01T12:34:56Z" |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "email_consent_change" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "customers_email_marketing_consent/update" |

### CUSTOMERS_MARKETING_CONSENT_UPDATE (SMS)の例示データ

|変数|例示値|
|---|---|
|`customer_id`|"6691629760567"|
| `consent_state` | "subscribed"|
| `opt_in_level` |"single_opt_in" |
| `consent_collected_from` | "website" |
| `consent_timestamp` | "2024-06-01T12:34:56Z" |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "sms_consent_change" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "customers_marketing_consent/update" |

### CUSTOMERS_CREATEの例示データ

|変数|例示値|
|---|---|
|`customer_id`|"6691629760567"|
|`customer_email`|"user.name@example.com"|
| `customer_first_name` | "John" |
| `customer_last_name` | "Smith" |
| `customer_city` | "San Diego" |
| `customer_country` | "US" |
| `customer_country_code` | "US" |
| `province` | "California" |
| `province_code` | "CA" |
| `order_currency` | "USD" |
| `shopify_tags` | "wholesale,newsletter" |
| `created_at` | "2024-06-01T12:34:56Z" |

#### Tealiumメタデータ

|変数|例示値|
|---|---|
| `tealium_event` | "Shopify New Customer" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "customers/create" |