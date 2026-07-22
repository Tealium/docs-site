---
title: AvantLink AvantMetrics Tag Setup Guide
description: This article describes how to set up the AvantLink AvantMetrics tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/avantlink-avantmetrics-tag/
---
This article describes how to set up the AvantLink AvantMetrics tag.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [about-tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Site ID**: The merchant site ID.
 
## Load rules

Load the tag on all pages or set conditions for when your tag loads. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `site_id` | String | Site ID. |
| `new_customer` | Boolean | Whether this is a new customer. |

### E-Commerce

| Variable | Type/Values | Description |
|:---------|:-----|:------------|
| `order_id` | String | Order ID (Overrides `_corder`). |
| `amount` | Number | The order subtotal amount (Overrides `_csubtotal`). |
| `currency` | String | Currency (Overrides `_ccurrency`). |
| `state` | String | State (Overrides `_cstate`). |
| `country` | String | Country (Overrides `_ccountry`). |
| `ecc` | String | Coupon code (Overrides `_cpromo`). |
| `tax` | Number | Amount of tax charged (Overrides `_ctax`). |
| `shipping` | Number | Amount of shipping fees charged (Overrides `_cship`). |
| `parent_sku` | Array | Parent SKU IDs (Overrides `_cprod`). |
| `variant_sku` | Array | Variant SKU IDs (Overrides `_csku`). |
| `price` | Array | SKU prices (Overrides `_cprice`). |
| `qty` | Array | SKU quantities (Overrides `_cquan`). |