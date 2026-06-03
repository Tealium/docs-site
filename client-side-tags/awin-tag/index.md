---
title: Awin Tag Setup Guide
description: This article describes how to set up the Awin tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/awin-tag/
---
## Tag Tips

* We recommend a hybrid setup using both a tag and a connector. This configuration ensures maximum data resilience, improves event matching with server-side signals, and maintains data flow continuity while retaining real-time client-side signals. For more information, see [Awin Conversions Connector]().
* Use mapping to:  
  * Override the standard config values. 
  * Override the E-Commerce extension values.
  * Pass custom parameters.
  * Setup event triggers.
* Supports the following E-Commerce extension values:  
  * Order ID.  
  * Order total.  
  * Order sub total.  
  * Order shipping.  
  * Order tax.  
  * Order currency.  
  * List of product IDs.  
  * List of categories.  
  * List of quantities.  
  * List of prices.
* An order is recorded if the Order ID value is set.
* The default value for the commission group is `DEFAULT`.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Awin tag. For more information, see [Manage tags]()).

After adding the tag, configure the following settings:

* **Advertiser ID**: Your Awin-provided advertiser ID.
* **Add Product Level Data**: Add the product-level data to the data payload.
* **Is Test**: Select this option to test the tag.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable | Type | Description |
|:-------------|:---------|:---------|
| `advertiser_id`    | String  | Advertiser ID.          |
| `add_products`     | Boolean | Add product level data. |
| `channel`          | String  | Channel.                |
| `commission_group` | String  | Commission group        |
| `is_test`          | Boolean | Is test.                |
| `custom`           | Array   | Custom values array.    |
| `custom.#`         | String  | You can map a maximum of 255 custom parameters. Each parameter follows the naming convention `custom.#`, where `#` is a number from `11` to `255`. For example: `custom.1`, `custom.2`, etc.       |

#### E-Commerce

| Variable | Type | Description |
|:-------------|:---------|:---------|
| `order_id` (Overrides `_corder`)          | String | Order ID. |
| `order_subtotal` (Overrides `_csubtotal`) | Number | Sub total/Total amount. |
| `order_currency` (Overrides `_ccurrency`) | String | Currency. |
| `order_coupon_code` (Overrides `_cpromo`) | String | Promo code.  |
| `product_id` (Overrides `_cprod`)         | Array  | List of product IDs. |
| `product_name` (Overrides `_cprodname`)   | Array  | List of names.    |
| `product_sku` (Overrides `_csku`)         | Array  | List of SKUs. |
| `product_category` (Overrides `_ccat`)    | Array  | List of Categories. |
| `product_quantity` (Overrides `_cquan`)   | Array  | List of quantities. |
| `product_unit_price` (Overrides `_cprice`)| Array  | List of prices.  |
| `product_commission`                      | Array  | List of commission groups. |

#### Event Triggers

| Variable   | Type | Description  |
|:-----------|:-------------|:-------------|
| `conversion` | String | Conversion. |

### Vendor Documentation

* [Awin: Why hybrid tracking is essential for your affiliate programme](https://advertiser-success.awin.com/s/article/Why-hybrid-tracking-is-essential-for-your-affiliate-programme-here-s-what-you-need-to-know)
* [Awin: Advertiser Mastertag](https://developer.awin.com/docs/advertiser-mastertag)
