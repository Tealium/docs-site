---
title: Logicad Tag Setup Guide
description: This article describes how to set up the Logicad Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/logicad-tag/
---
Logicad enables you to effectively transmit advertisements with large-scale delivery log and system infrastructure which processes audience data fast and stable using its own algorithm.

## Tag tips

* Product Group ID and Advertiser Product ID mappings are required for Dynamic Creative Retargeting tag types.
* Product Group ID mapping is required for the Dynamic Creative Conversion tag type.
* Supports these E-Commerce extension parameters:
    * Order ID (`_corder`)
    * Sub Total (`_csubtotal`)
    * List of Product IDs (`_cprod`)
    * List of Quantities (`_cquan`)
    * List of Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Advertiser ID**: Your So-net Media Network provided Advertiser ID.
* **Tag Type**: Select the type of tag for your business case.
* **Field Delimiter**: The delimiter between product field information. Can not be the same as record delimiter.
* **Record Delimiter**: The delimiter between product record information. Can not be the same as field delimiter.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

The available categories are:

### Standard

| Variable | Description |
|---|---|
| `advertiser_id` | Advertiser ID |
| `type` | Tag type |
| `field_delim` | Product field delimiter |
| `record_delim` | Product record delimiter |
| `product_group_id` | Product group ID |
| `advertiser_product_id` | Advertiser product ID |
| `retargeting_param` | Retargeting parameter |
| `log_param1` | Log parameter 1 |
| `log_param2` | Log parameter 2 |
| `log_param3` | Log parameter 3 |
| `log_param4` | Log parameter 4 |
| `log_param5` | Log parameter 5 |
| `log_param6` | Log parameter 6 |
| `log_param7` | Log parameter 7 |
| `log_param8` | Log parameter 8 |
| `log_param9` | Log parameter 9 |
| `log_param10` | Log parameter 10 |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| `order_id` | Order ID  (Overrides `_corder`) |
| `order_subtotal` | Total price/sub total  (Overrides `_csubtotal`) |
| `order_quantity` | Total quantity  (Overrides sum of product_quantity) |
|`product_id`  List of product IDs (Overrides `_cprod`)  | 
| `product_quantity` | List of quantities (Overrides `_cquan`)  | 
| `product_unit_price` | List of prices (Overrides `_cprice`)  |

