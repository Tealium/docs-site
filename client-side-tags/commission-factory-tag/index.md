---
title: Commission Factory Tag Setup Guide
description: This article describes how to add and configure the Commission Factory marketplace tag.
url: https://docs.tealium.com/client-side-tags/commission-factory-tag/
---
## Requirements

* The Commission Factory tag requires the [E-Commerce extension]().
* You must add the extension and map the `_corder`, `_csubtotal`, `_csku`, `_cprice,` `_cquan` variables to their corresponding data sources.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Tag ID**: An integer value provided by Commission Factory.
* **CF-Object Name**: The variable used to execute commands. The default value is **cf**.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information about load rules, see [About load rules]().

## Data mappings

Mappings for this tag are handled automatically by the E-Commerce extension.

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:-----|:------------|
| `tag_id` | String  | Tag ID |
| `namespace` | String  |CF-Object name |

### E-Commerce

| Variable | Type | Description |
|:---------|:-----|:------------|
| `reference` | String  | Reference 1 |
| `reference2` | String | Reference 2 |
| `reference3` | String | Reference 3 |
| `reference4` | String | Reference 4 |
| `customer_type` | String | Customer type |
| `order_id` | String | Order ID (Overrides `_corder`) |
| `order_subtotal` |String  | Sub total/Amount (Overrides `_csubtotal`) |
| `order_currency` |String  | Currency (Overrides `_ccurrency`) |
| `order_coupon_code` |String  | Promo code/Coupon (Overrides `_cpromo`) |
| `product_sku` | Array | List of SKUs (Overrides `_csku`) |
| `product_quantity` | Array | List of quantities (Overrides `_cquan`) |
| `product_unit_price` | Array | List of prices (Overrides `_cprice`) |