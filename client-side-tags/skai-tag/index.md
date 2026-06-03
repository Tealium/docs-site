---
title: Skai (formerly Kenshoo) Tag
description: This article describes how to set up the Skai (formerly Kenshoo) tag.
url: https://docs.tealium.com/client-side-tags/skai-tag/
---
## Tag Tips

* You may dynamically overwrite or set the tag configurations with mappings.
* To trigger conversion tracking, you must set `cid`, `conversion_code`, and `conversionType`. The `conversionType` parameter defaults to &#39;conv&#39; if not otherwise set.
* To track custom parameters, you must map to custom destinations.
* Supports these E-Commerce extension parameters:
    * Order ID (`_corder`)
    * Order Subtotal (`_csubtotal`)
    * Order Currency (`_ccurrency`)
    * Order Coupon Code (`_cpromo`)

## Tag Configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Customer ID**: Your Skai Customer ID.
* **Conversion Code**: The Skai-provided Conversion Code.
* **Conversion Type**: The conversion type. Defaults to &#39;conv&#39; if not set.

## Load Rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data Mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| `cid` | Customer ID |
| `conversion_code` | Conversion code |
| `conversionType` | Conversion type |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` | Order ID (Overrides `_corder`) |
| `order_subtotal` | Sub total (Overrides `_csubtotal`) |
| `order_currency` | Currency (Overrides `_ccurrency`) |
| `order_coupon_code` | Promo code (Overrides `_cpromo`) |