---
title: Tealium configuration
description: This article provide information about the Tealium configuration steps that should be completed before installing the Tealium Shopify app.
url: https://docs.tealium.com/platforms/shopify/tealium-shopify-configuration/
---
To send event data to Tealium iQ Tag Management or Tealium EventStream API Hub from the Tealium Shopify app, the following are needed:

* A Tealium HTTP API data source
* Event specifications for events to be sent to EventStream and for the data source
* A data layer variable named `restock`

The data source, data source event specification, and data layer variable are used during installation of the Tealium app, and should be created before installing the app.

## Create a `restock` variable

Create a boolean data layer variable named `restock`. For more information about creating a data layer variable, see [Add a variable](https://docs.tealium.com/manage-variables/#add-a-variable).

## Create event specifications

For more information about creating event specifications, see [Manage event specifications]().

### Shopify refund event specification

Create a `shopify_refund` event specification and add the following universal data object attributes to the event specification: 

| Attribute Name | Data Type |
|----|----|-----|
| `customer_id` | String |
| `note` | String |
| `order_currency` | String |
| `order_discount` | Number |
| `order_id` | String |
| `order_tax` | Number |
| `order_total` | Number |
| `product_category` | Array of strings |
| `product_id` | Array of strings |
| `product_name` | Array of strings |
| `product_quantity` | Array of numbers |
| `product_sku` | Any |
| `product_unit_price` | Array of numbers |
| `restock` | Boolean |

### Shopping cart event specifications

Create `cart_add` and  `cart_remove` event specifications and add the following universal data object attributes to the event specifications: 

| Attribute Name          | Data Type          |
|-------------------------|--------------------|
| `cart_total_items`       | Number             |
| `cart_total_value`       | Number             |
| `customer_logged_in`     | Boolean            |
| `language_code`          | String             |
| `page_name`              | String             |
| `page_type`              | String             |
| `product_brand`          | Array of strings   |
| `product_category`       | String             |
| `product_currency`       | String             |
| `product_id`             | Array of strings   |
| `product_image_url`      | Array of strings   |
| `product_main_id`        | Array of numbers   |
| `product_name`           | Array of strings   |
| `product_normal_price`   | Array of numbers   |
| `product_one_variant`    | Array of booleans  |
| `product_quantity`       | Array of numbers   |
| `product_unit_price`     | Array of numbers   |
| `product_url`            | String             |
| `tealium_visitor_id`     | String             |

### Purchase event specification

Create a `purchase` event specification and add the following universal data object attributes to the event specification:

|Attribute Name|Data Type |Example Value|
|---|-----|----|
| `site_section`| String | "order" |
| `tealium_from_checkout`| integer | 1 |
| `customer_country`| String| "CA" |
| `customer_state`| String | "AB" |
| `customer_city`| String | "Calgary" |
| `customer_zip`| String | "T2J 6P4" |
| `customer_id`| String | "6691629760567" |
| `customer_logged_in`| Boolean | "false" |
| `customer_email`| String | "user.name@example.com"|
| `customer_first_name`| String | "user" |
| `customer_last_name`| String | "name" |
| `country_code`| String | "CA" |
| `order_id`| String | "5853792796727"|
| `order_subtotal`| Number | 2400 |
| `order_total`| Number | 2400 |
| `order_currency`| String | "CAD" |
| `order_tax`| Number | 0 |
| `order_shipping`| Number | 0 |
| `order_discount_amount` | String | "" |
| `payment_gateway`| String | "shopify_payments" |
| `product_id`| Array of Strings | ["6933873000503"] |
| `product_on_page`| Array of Strings | ["6933873000503"] |
| `product_quantity`| Array of Numbers | [4] |
| `product_unit_price`| Array of Numbers | [2400] |
| `product_name`| Array of Strings | ["Dress Shirts"] |
| `product_sku`| Array of Numbers | ["40586935402551"] |
| `page_name`| String | "Information - Tealiumapp - Checkout"|
| `cart_total_items`| Number | 1 |
| `cart_total_value`| Number | 2400 |
| `page_type`| String | "order" |
| `tealium_event` | String | "purchase" |
| `tealium_visitor_id` | String | "01902bf47c7200111b70236f67ee0506f004b06700fbe" |

## Create an HTTP API data source

Create an HTTP API data source with the following event specifications:

* `cart_add`
* `cart_remove`
* `checkout`
* `purchase`
* `shopify_refund`

For more information about creating a data source, see [Create a data source]().

Save and publish your changes.