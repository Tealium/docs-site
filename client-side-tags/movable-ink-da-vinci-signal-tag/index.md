---
title: Movable Ink Da Vinci Signal Tag Setup Guide
description: This article describes how to set up the Movable Ink Da Vinci Signal tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/movable-ink-da-vinci-signal-tag/
---
## Tag tips

* Use mappings to:   
  * Dynamically override configuration data   
  * Dynamically override the E-Commerce extension values   
  * Send additional data values   
  * Event trigger
* Supports the following E-Commerce extension values:   
  * Customer ID   
  * Order ID   
  * Order Sub Total   
  * List of Product Discounts   
  * List of Product IDs   
  * List of Product Names   
  * List of Product Quantities   
  * List of Product Prices

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Access Token**: Da Vinci Signal API access token.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

For more information on the events and expected event details, see the [Da Vinci Javascript SDK documentation](https://help.coherentpath.com/guides/technical/javascript-sdk). You must be logged into the Da Vinci Help Center to access the documentation. If there are any issues accessing, contact your Da Vinci account team.

The available categories are:

### Tag Configuration

|Variable| Type | Description|
|---| ---|---|
| `config_access_token`| String| Access token. | 
| `config_base_url` | String | Base URL (The default value is `https://track.coherentpath.com`.) |
| `config_currency_code` | String | Currency code (The default value is `USD`.)|
| `config_debug` | Boolean | Debug flag (The default value is `false`.)|

### Event Parameters

|Variable| Type | Description|
|---| ---| ---|
| `contact_id`| String | Contact ID.  |
| `customer_email`| String| Customer email. |
| `order_discount`| String| Order discount. |
| `order_processed_at` | String| Order processed date. (The default value is the current time.) |
| `page_referrer` | String| Page referrer. (The default value is the current page referrer.)|
| `page_title` | String| Page title. (The default value is the current page title.) |
| `page_url` | String| Page URL. (The default value is the current page URL.) |
| `product_variant_id`| Array| List of product variant IDs. |
| `product_variant_name`| Array| List of product variant names. |
| `product_variant_price`| Array| List of product variant prices.|
| `product_variant_product_id` | Array| List of product variant's product IDs. (Links Product Variant to Product.) |
| `search_term`| String| Search term.|
| `source`| String| How the user arrived at the page. |
| `metadata_tags`| Array| List of metadata tags. |
| `metadata_attributes`| Object| Metadata attributes. |

### E-Commerce

|Variable| Type | Description|
|---| ---|---|
| `customer_id` (Overrides `_ccustid`)| String| Customer ID. |
| `order_id` (Overrides `_corder`)| String| Order ID. |
| `order_subtotal` (Overrides `_csubtotal`)| String| Order subtotal. |
| `product_discount` (Overrides `_cpdisc`)| Array| List of product discounts. |
| `product_id` (Overrides `_cprod`)| Array| List of product IDs. |
| `product_name` (Overrides `_cprodname`)| Array| List of product names. |
| `product_quantity` (Overrides `_cquan`)| Array| List of product quantities. | 
| `product_unit_price` (Overrides `_cprice`)| Array| List of product prices. |

### Events

|Variable| Description|
|---| ---|
|`Forget`| Forget|
|`Identity`| Identity|
|`OrderCancelation`| Order Cancelation|
|`OrderCompletion`| Order Completion|
|`OrderRefund`| Order Refund|
|`PageView`| Page View|
|`ProductPageView`| Product Page View|
|`ProductSearch`| Product Search|
