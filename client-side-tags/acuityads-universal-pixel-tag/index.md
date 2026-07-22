---
title: AcuityAds Universal Pixel Setup Guide
description: This article describes how to set up the AcuityAds Universal Pixel Tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/acuityads-universal-pixel-tag/
---
With the Acuity tag, you can systematically and mathematically take the risk, mystery and waste out of the media buying process to ensure – and even prove – that every advertising dollar can be spent wisely and well.

## Tag tips

* Use mappings to override the value for Pixel Key or E-commerce variables and set **Page Group Number**.

* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Order Total (`_ctotal`) Product ID (`_cprod`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Pixel Key**: The pixel's unique key-value.

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Description |
|:---------|:------------|
| Pixel Key `pixel_key`  | String |
| Page Group Number `page_group_number`  | Number |

### E-Commerce

| Variable | Description |
|:---------|:------------|
| Order ID  | `order_id` (Overrides `_corder`) Number  |
| Order Total/Cart Revenue  | `order_total` (Overrides `_ctotal`) Number |
| List of Product IDs `product_id` (Overrides `_cprod`)  | Array |

    