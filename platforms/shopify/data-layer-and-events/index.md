---
title: Data layer and events
description: This article provides information about the data layer variables and events tracked by the Tealium Shopify app.
url: https://docs.tealium.com/platforms/shopify/data-layer-and-events/
---
For more information about the Tealium data layer and the Universal Data Object, see [An introduction to the data layer](https://docs.tealium.com/an-introduction-to-the-data-layer/) and [Universal Data Object](https://docs.tealium.com/universal-data-object/).

## Supported variables

The following universal data layer variables are supported for the Tealium Shopify app:

|Variable|Description|
|---|---|
|`cart_total_items`|integer|
|`cart_total_value`|float|
|`country_code`|string|
|`customer_city`|string|
|`customer_country`|string|
|`customer_email`|string|
|`customer_first_name`|string|
|`customer_id`|string|
|`customer_last_name`|string|
|`customer_logged_in`|boolean|
|`customer_state`|string|
|`customer_zip`|string|
|`language_code`|string|
|`order_currency`|string|
|`order_discount_amount`|string|
|`order_id`|string|
|`order_shipping`|float|
|`order_subtotal`|float|
|`order_tax`|float|
|`order_total`|float|
|`page_name`|string|
|`page_type`|string|
|`payment_gateway`|string|
|`product_brand`|list|
|`product_category`|list|
|`product_currency`|string|
|`product_id`|list|
|`product_image_url`|list|
|`product_main_id`|list|
|`product_name`|list|
|`product_normal_price`|list|
|`product_on_page`|list|
|`product_one_variant`|list|
|`product_price`|list|
|`product_quantity`|list|
|`product_sku`|list|
|`product_unit_price`|list|
|`product_url`|list|
|`search_keyword`|string|
|`search_results`|integer|
|`site_section`|string|
|`tealium_event`|string|
|`tealium_from_checkout`|integer|
|`tealium_visitor_id`|string|

## Client-side example data

The following sections show example data for specific events.

### Example data for page_view and category_view events

|Variable|Example Value|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`page_name`|"Women's Clothing"|
|`page_type`|"page"|
|`product_on_page`|["40586935271479", "40586935664695", "40586935599159", "40586935402551", "40586935762999",…]|
|`site_section`|"collection"|
|`tealium_event`|"page_view"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

### Example data for product_view events

|Variable|Example Value |
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`page_name`|"Women's Shoes"|
|`page_type`|"product"|
|`product_brand`|["XYZ Shoes"]|
|`product_id`|["6933873000503"]|
|`product_name`|["Flats"]|
|`product_price`|["600.00"]|
|`product_sku`|[""]|
|`site_section`|"product"|
|`tealium_event`|"product_view"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

#### Example data for cart_add / cart_remove

|Variable|Example Value|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`page_name`|"Women's Clothing"|
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

### Example data for search events

|Variable|Example Value|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|"false"|
|`language_code`|"en"|
|`search_keyword`|"shoes"|
|`search_results`|12|
|`site_section`|"search"|
|`page_name`|"Search: 12 results found for &quot;shoes&quot;"|
|`product_on_page`|["40586935009335", "40586935566391", "40586935500855", "40586934976567", "40586935402551",…]|
|`tealium_event`|"search"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

### Example data for checkout events

|Variable|Example Value|
|---|---|
| `site_section` | "order" |
| `tealium_from_checkout` | 1 |
| `page_name` | "Checkout : Started" |
| `page_type` | "checkout" |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | "checkout" |
| `tealium_visitor_id` | "01902bf47c7200111b70236f67ee0506f004b06700fbe" |

### Example data for checkout_address_info_submitted events

|Variable|Example Value|
|---|---|
| `site_section` | "order" |
| `tealium_from_checkout` | 1 |
| `page_name` | "Checkout : Form" |
| `page_type` | "checkout" |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | "checkout_address_info_submitted" |
| `tealium_visitor_id` | "01902bf47c7200111b70236f67ee0506f004b06700fbe" |

### Example data for purchase events

|Variable|Example Value|
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
|`page_name`|"Information - Tealiumapp - Checkout"|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`page_type`|"order"|
|`tealium_event`|"purchase"|
|`tealium_visitor_id`|"01902bf47c7200111b70236f67ee0506f004b06700fbe"|

## Webhook example data

The following sections show example data for specific events.

### Example data for ORDERS_CREATE

#### Order Identifiers

|Variable|Example Value|
|---|---|
| `order_id` |  "5853792796727" |
| `order_name` | "Order #12345" |
| `order_number` | "12345" |
| `checkout_token` | "abcdef123456" |
| `confirmation_number` | "CONF123456" |
| `landing_site` | "/landing-page" |
| `order_created_at` | "2024-06-01T12:34:56Z" |

#### Order Financials

|Variable|Example Value|
|---|---|
|`order_total`|2400|
|`order_subtotal`|2400|
| `order_discount` | 0 |
| `order_tax` | 0 |
| `order_shipping` | 0 |
| `order_currency` | "USD" |
| `order_payment_type` | "VISA""|
| `order_coupon_code` | "20SAVE"" |
| `order_shipping_type` | "Fedex" |

#### Customer Data

|Variable|Example Value|
|---|---|
|`customer_id`|"6691629760567"|
|`customer_email`|"user.name@example.com"|
| `customer_first_name` | "John"" |
| `customer_last_name` | "Smith" |
| `customer_city` | "San Diego" |
| `customer_country` | "US" |
| `customer_state` | "CA" |
| `customer_zip` | "92121" |
| `customer_email_marketing_consent` | "True" |
| `customer_sms_marketing_consent` | "True" |

#### Product Data (Arrays - one entry per line item)

|Variable|Example Value|
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

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "purchase" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "orders/create" |

### Example data for CHECKOUTS_CREATE

|Variable|Example Value|
|---|---|
| `order_id` |  "5853792796727" |
| `checkout_token` | "abcdef123456" |
| `order_total` | 2400 |
| `order_subtotal` | 2400 |
| `order_discount` | 0 |
| `order_currency` | "USD" |

#### Product Data (Arrays)

|Variable|Example Value|
|---|---|
| `product_id` | ["6933873000503"] |
| `product_variant` | ["Size 8 / Black"] |
| `product_name` | ["XYZ Women's Flats"] |
| `product_quantity` | [4] |
| `product_sku` | ["40586935402551"] |
| `product_category` | ["Women's Shoes"] |
| `product_discount` | [0] |
| `product_list_price` | [2400] |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "checkouts_create" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "checkouts/create" |

### Example data for REFUNDS_CREATE 

|Variable|Example Value|
|---|---|
| `order_id` |  "5853792796727" |
|`customer_id`|"6691629760567"|
| `order_currency` | "USD" |
|`order_total`|2400|
| `order_tax` | 0 |
| `order_discount` | 0 |
| `restock` | true |
| `note` | String (refund reason) |

#### Refunded Products (Arrays)

|Variable|Example Value|
|---|---|
|Variable|Example Value|
|---|---|
| `product_id` | ["6933873000503"] |
| `product_variant` | ["Size 8 / Black"] |
| `product_sku` | ["40586935402551"] |
| `product_quantity` | [2] |
| `product_name` | ["XYZ Women's Flats"] |
| `product_unit_price` | [2400] |
| `product_category` | ["Women's Shoes"] |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "shopify_refund" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "refunds/create" |

### Example data for CARTS_CREATE / CARTS_UPDATE

|Variable|Example Value|
|---|---|
| `cart_token` | "abcdef123456" |
| `cart_total_items` | 2 |
| `cart_total_value` | 1200 |

#### Product Data (Arrays)

|Variable|Example Value|
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

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "cart_create" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "carts/create" |

### Example data for CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATE

|Variable|Example Value|
|---|---|
|`customer_id`|"6691629760567"|
|`customer_email`| "user.name@example.com"|
| `consent_state` | "subscribed"  |
| `opt_in_level` | "single_opt_in"  |
| `consent_timestamp` | "2024-06-01T12:34:56Z" |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "email_consent_change" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "customers_email_marketing_consent/update" |

### Example data for CUSTOMERS_MARKETING_CONSENT_UPDATE (SMS)

|Variable|Example Value|
|---|---|
|`customer_id`|"6691629760567"|
| `consent_state` | "subscribed"|
| `opt_in_level` |"single_opt_in" |
| `consent_collected_from` | "website" |
| `consent_timestamp` | "2024-06-01T12:34:56Z" |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "sms_consent_change" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "customers_marketing_consent/update" |

### Example data for CUSTOMERS_CREATE

|Variable|Example Value|
|---|---|
|`customer_id`|"6691629760567"|
|`customer_email`|"user.name@example.com"|
| `customer_first_name` | "John"" |
| `customer_last_name` | "Smith" |
| `customer_city` | "San Diego" |
| `customer_country` | "US" |
| `customer_country_code` | "US" |
| `province` | "California" |
| `province_code` | "CA" |
| `order_currency` | "USD" |
| `shopify_tags` | "wholesale,newsletter" |
| `created_at` | "2024-06-01T12:34:56Z" |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | "Shopify New Customer" |
| `tealium_account` | "myaccount" |
| `tealium_profile` | "main" |
| `tealium_datasource` | "shopify_app" |
| `shopify_topic` | "customers/create" |