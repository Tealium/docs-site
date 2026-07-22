---
title: Kissmetrics Tag Setup Guide
description: This article describes how to set up the Kissmetrics tag.
url: https://docs.tealium.com/client-side-tags/kissmetrics-tag/
---
Kissmetrics is a powerful web analytics solution that helps you to increase customer acquisition and retention rates, make smarter business decisions, and boost your bottom line.

## Tag tips

* Use mapping to:
    * Override the standard config value for KM API Key
    * Override the E-Commerce extension values
    * Trigger calls containing the mapped data to` _kmq.push()`
* Purchase events are automatically recorded when an order ID is set. All of the E-Commerce extension values are supported.
* `_kmq.push` mapping examples:
    * `['record', 'EVENT_NAME']`
    * `['record', 'EVENT_NAME', {'PROPERTY_NAME':'VALUE'}]`
    * `['record', 'EVENT_NAME', {'PROPERTY_NAME':'VALUE'}, CALLBACK_FUNCTION]`
    * `['set', {'PROPERTY_NAME':'VALUE'}]`
    * `['identify', 'IDENTITY']`
* Common Methods: [Kissmetrics API Common Metrics](https://support.kissmetrics.io/docs/common-methods).

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **KM API Key**: The long string of letters and numbers in the URL from KISSmetrics. For example, `//doug1izaerwt3.cloudfront.net/YOUR_API_KEY.1.js`.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `kmkey`  | API Key |
| `kmq_push` | Trigger the call to push all the data queued in the Kissmetrics Queue (`kmq`). |

### E-Commerce

| Variable | Type | Description |
|:---------|:------------|:------------|
| `order_id` (Overrides `_corder`) |Text |Order ID  |
| `order_total` (Overrides `_ctotal`) | Text |Order total  |
| `order_subtotal` (Overrides `_csubtotal`) | Text | Sub total  | 
| `shipping_amt` (Overrides `_cship`) | Text |Shipping amount  |
| `tax_amt` (Overrides `_ctax`) | Text |Tax amount  | 
| `store` (Overrides `_cstore`) | Text |Store  | 
| `currency` (Overrides `_ccurrency`) | Text |Currency  |
| `promocode` (Overrides `_cpromo`) | Text |Promo code  | 
| `cart_type` (Overrides `_ctype`) |Text |Cart or order type  |
| `custid` (Overrides `_ccustid`) | Text |Customer ID  |
| `city` (Overrides `_ccity`) | Text |Customer city  | 
| `state` (Overrides `_cstate`) | Text |Customer state  |
| `zip` (Overrides `_czip`) |  Text |Customer ZIP Code | 
| `country` (Overrides `_ccountry`) | Text | Customer country  |
| `product_ids` (Overrides `_cprod`)  | Array |  List of Product IDs |
| `product_names` (Overrides `_cprodname`)  | Array | List of names |
| `product_skus` (Overrides `_csku`)  | Array | List of SKUs |
| `product_brands` (Overrides `_cbrand`)  | Array | List of brands |
| `product_categories` (Overrides `_ccat`)  | Array | List of categories |
| `product_categories2` (Overrides `_ccat2`)  | Array | List of categories 2 |
| `product_quantities` (Overrides `_cquan`)  | Array | List of quantities |
| `product_prices` (Overrides `_cprice`)  | Array | List of prices |
| `product_discounts` (Overrides `_cpdisc`)  | Array | List of discounts |

