---
title: Data layer and events
description: This article provides information about the data layer variables and events tracked by the Tealium Shopify app.
url: https://docs.tealium.com/platforms/shopify/data-layer-and-events/
---
For more information about the Tealium data layer and the Universal Data Object, see [An introduction to the data layer]() and [Universal Data Object]().

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
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`page_name`|&#34;Women&#39;s Clothing&#34;|
|`page_type`|&#34;page&#34;|
|`product_on_page`|[&#34;40586935271479&#34;, &#34;40586935664695&#34;, &#34;40586935599159&#34;, &#34;40586935402551&#34;, &#34;40586935762999&#34;,…]|
|`site_section`|&#34;collection&#34;|
|`tealium_event`|&#34;page_view&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

### Example data for product_view events

|Variable|Example Value |
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`page_name`|&#34;Women&#39;s Shoes&#34;|
|`page_type`|&#34;product&#34;|
|`product_brand`|[&#34;XYZ Shoes&#34;]|
|`product_id`|[&#34;6933873000503&#34;]|
|`product_name`|[&#34;Flats&#34;]|
|`product_price`|[&#34;600.00&#34;]|
|`product_sku`|[&#34;&#34;]|
|`site_section`|&#34;product&#34;|
|`tealium_event`|&#34;product_view&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

#### Example data for cart_add / cart_remove

|Variable|Example Value|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`page_name`|&#34;Women&#39;s Clothing&#34;|
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

### Example data for search events

|Variable|Example Value|
|---|---|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`customer_logged_in`|&#34;false&#34;|
|`language_code`|&#34;en&#34;|
|`search_keyword`|&#34;shoes&#34;|
|`search_results`|12|
|`site_section`|&#34;search&#34;|
|`page_name`|&#34;Search: 12 results found for &amp;quot;shoes&amp;quot;&#34;|
|`product_on_page`|[&#34;40586935009335&#34;, &#34;40586935566391&#34;, &#34;40586935500855&#34;, &#34;40586934976567&#34;, &#34;40586935402551&#34;,…]|
|`tealium_event`|&#34;search&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

### Example data for checkout events

|Variable|Example Value|
|---|---|
| `site_section` | &#34;order&#34; |
| `tealium_from_checkout` | 1 |
| `page_name` | &#34;Checkout : Started&#34; |
| `page_type` | &#34;checkout&#34; |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | &#34;checkout&#34; |
| `tealium_visitor_id` | &#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34; |

### Example data for checkout_address_info_submitted events

|Variable|Example Value|
|---|---|
| `site_section` | &#34;order&#34; |
| `tealium_from_checkout` | 1 |
| `page_name` | &#34;Checkout : Form&#34; |
| `page_type` | &#34;checkout&#34; |
|`cart_total_items`|0|
|`cart_total_value`|0.00|
| `tealium_event` | &#34;checkout_address_info_submitted&#34; |
| `tealium_visitor_id` | &#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34; |

### Example data for purchase events

|Variable|Example Value|
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
|`page_name`|&#34;Information - Tealiumapp - Checkout&#34;|
|`cart_total_items`|0|
|`cart_total_value`|0.00|
|`page_type`|&#34;order&#34;|
|`tealium_event`|&#34;purchase&#34;|
|`tealium_visitor_id`|&#34;01902bf47c7200111b70236f67ee0506f004b06700fbe&#34;|

## Webhook example data

The following sections show example data for specific events.

### Example data for ORDERS_CREATE

#### Order Identifiers

|Variable|Example Value|
|---|---|
| `order_id` |  &#34;5853792796727&#34; |
| `order_name` | &#34;Order #12345&#34; |
| `order_number` | &#34;12345&#34; |
| `checkout_token` | &#34;abcdef123456&#34; |
| `confirmation_number` | &#34;CONF123456&#34; |
| `landing_site` | &#34;/landing-page&#34; |
| `order_created_at` | &#34;2024-06-01T12:34:56Z&#34; |

#### Order Financials

|Variable|Example Value|
|---|---|
|`order_total`|2400|
|`order_subtotal`|2400|
| `order_discount` | 0 |
| `order_tax` | 0 |
| `order_shipping` | 0 |
| `order_currency` | &#34;USD&#34; |
| `order_payment_type` | &#34;VISA&#34;&#34;|
| `order_coupon_code` | &#34;20SAVE&#34;&#34; |
| `order_shipping_type` | &#34;Fedex&#34; |

#### Customer Data

|Variable|Example Value|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_email`|&#34;user.name@example.com&#34;|
| `customer_first_name` | &#34;John&#34;&#34; |
| `customer_last_name` | &#34;Smith&#34; |
| `customer_city` | &#34;San Diego&#34; |
| `customer_country` | &#34;US&#34; |
| `customer_state` | &#34;CA&#34; |
| `customer_zip` | &#34;92121&#34; |
| `customer_email_marketing_consent` | &#34;True&#34; |
| `customer_sms_marketing_consent` | &#34;True&#34; |

#### Product Data (Arrays - one entry per line item)

|Variable|Example Value|
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

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;purchase&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;orders/create&#34; |

### Example data for CHECKOUTS_CREATE

|Variable|Example Value|
|---|---|
| `order_id` |  &#34;5853792796727&#34; |
| `checkout_token` | &#34;abcdef123456&#34; |
| `order_total` | 2400 |
| `order_subtotal` | 2400 |
| `order_discount` | 0 |
| `order_currency` | &#34;USD&#34; |

#### Product Data (Arrays)

|Variable|Example Value|
|---|---|
| `product_id` | [&#34;6933873000503&#34;] |
| `product_variant` | [&#34;Size 8 / Black&#34;] |
| `product_name` | [&#34;XYZ Women&#39;s Flats&#34;] |
| `product_quantity` | [4] |
| `product_sku` | [&#34;40586935402551&#34;] |
| `product_category` | [&#34;Women&#39;s Shoes&#34;] |
| `product_discount` | [0] |
| `product_list_price` | [2400] |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;checkouts_create&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;checkouts/create&#34; |

### Example data for REFUNDS_CREATE 

|Variable|Example Value|
|---|---|
| `order_id` |  &#34;5853792796727&#34; |
|`customer_id`|&#34;6691629760567&#34;|
| `order_currency` | &#34;USD&#34; |
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
| `product_id` | [&#34;6933873000503&#34;] |
| `product_variant` | [&#34;Size 8 / Black&#34;] |
| `product_sku` | [&#34;40586935402551&#34;] |
| `product_quantity` | [2] |
| `product_name` | [&#34;XYZ Women&#39;s Flats&#34;] |
| `product_unit_price` | [2400] |
| `product_category` | [&#34;Women&#39;s Shoes&#34;] |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;shopify_refund&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;refunds/create&#34; |

### Example data for CARTS_CREATE / CARTS_UPDATE

|Variable|Example Value|
|---|---|
| `cart_token` | &#34;abcdef123456&#34; |
| `cart_total_items` | 2 |
| `cart_total_value` | 1200 |

#### Product Data (Arrays)

|Variable|Example Value|
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

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;cart_create&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;carts/create&#34; |

### Example data for CUSTOMERS_EMAIL_MARKETING_CONSENT_UPDATE

|Variable|Example Value|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_email`| &#34;user.name@example.com&#34;|
| `consent_state` | &#34;subscribed&#34;  |
| `opt_in_level` | &#34;single_opt_in&#34;  |
| `consent_timestamp` | &#34;2024-06-01T12:34:56Z&#34; |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;email_consent_change&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;customers_email_marketing_consent/update&#34; |

### Example data for CUSTOMERS_MARKETING_CONSENT_UPDATE (SMS)

|Variable|Example Value|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
| `consent_state` | &#34;subscribed&#34;|
| `opt_in_level` |&#34;single_opt_in&#34; |
| `consent_collected_from` | &#34;website&#34; |
| `consent_timestamp` | &#34;2024-06-01T12:34:56Z&#34; |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;sms_consent_change&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;customers_marketing_consent/update&#34; |

### Example data for CUSTOMERS_CREATE

|Variable|Example Value|
|---|---|
|`customer_id`|&#34;6691629760567&#34;|
|`customer_email`|&#34;user.name@example.com&#34;|
| `customer_first_name` | &#34;John&#34;&#34; |
| `customer_last_name` | &#34;Smith&#34; |
| `customer_city` | &#34;San Diego&#34; |
| `customer_country` | &#34;US&#34; |
| `customer_country_code` | &#34;US&#34; |
| `province` | &#34;California&#34; |
| `province_code` | &#34;CA&#34; |
| `order_currency` | &#34;USD&#34; |
| `shopify_tags` | &#34;wholesale,newsletter&#34; |
| `created_at` | &#34;2024-06-01T12:34:56Z&#34; |

#### Tealium Metadata

|Variable|Example Value|
|---|---|
| `tealium_event` | &#34;Shopify New Customer&#34; |
| `tealium_account` | &#34;myaccount&#34; |
| `tealium_profile` | &#34;main&#34; |
| `tealium_datasource` | &#34;shopify_app&#34; |
| `shopify_topic` | &#34;customers/create&#34; |