---
title: Skai (formerly Kenshoo) Tag
description: This article describes how to set up the Skai (formerly Kenshoo) tag.
url: https://docs.tealium.com/client-side-tags/skai-tag/
---
## Tag tips

* You may dynamically overwrite or set the tag configurations with mappings.
* To trigger conversion tracking, you must set `cid`, `conversion_code`, and `conversionType`. The `conversionType` parameter defaults to 'conv' if not otherwise set.
* To track custom parameters, you must map to custom destinations.
* Supports these E-Commerce extension parameters:
    * Order ID (`_corder`)
    * Order Subtotal (`_csubtotal`)
    * Order Currency (`_ccurrency`)
    * Order Coupon Code (`_cpromo`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Customer ID**: Your Skai Customer ID.
* **Conversion Code**: The Skai-provided Conversion Code.
* **Conversion Type**: The conversion type. Defaults to 'conv' if not set.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

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