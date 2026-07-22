---
title: United Internet Media (UIM) Retargeting Tag Setup Guide
description: This article describes how to set up the United Internet Media (UIM) Retargeting tag.
url: https://docs.tealium.com/client-side-tags/uim-tag/
---
## Tag tips

* Use mappings to override or dynamically set tag configurations.
* Use mappings to trigger events.
* Supports the following E-Commerce extension parameters:
    + Order ID (Overrides `_corder`)
    + Order Items (Overrides `_cprod`)
    + Order Total (Overrides `_ctotal`)
    + Order Shipping (Overrides `_cship`)
    + Order Currency (Overrides `_ccurrency`)
    + Product ID (Overrides `_cprod`)
    + Product Name (Overrides `_cprodname`)
    + Product Price (Overrides` _cprice`)
    + Product Currency (Overrides `_ccurrency`)
    + Basket Total (Overrides `_ctotal`)
    + Basket Items (Overrides `_cprod`)
    + Basket Currency (Overrides `_ccurrency`)



## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Advertiser**: Advertiser in JS URL. Required

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

| Variable | Type | Description |
|:---------|:------------|:------------|
|  `advertiser`  | String | Advertiser | 
|  `uuid_netid`  | String | UUID netid |
|  `privacy_law`  | String | Privacy Law |
|  `privacy_consent`  | String | Privacy Consent|

### E-Commerce

| Variable | Type |Description |
|:---------|:------------|:------------|
|  `page_name`  | String | Page Name |
|  `category_id`  | String | Category ID |
|  `category_name`  | String | Category Name |
|  `product_id` (Overrides `_cprod`)  | String | Product ID |
|  `product_name` (Overrides `_cprodname`)  | String | Product Name |
|  `product_price` (Overrides `_cprice`)  | String | Product Price |
|  `product_currency` (Overrides `_ccurrency`)  | String | Product Currency |
|  `basket_total` (Overrides `_ctotal`)  | String | Basket Total |
|  `basket_items` (Overrides `_cprod`)  | String | Basket Items |
|  `basket_currency` (Overrides `_ccurrency`)  | String | Basket Currency |
|  `order_id` (Overrides `_corder`)  | String | Order ID |
|  `order_items` (Overrides `_cprod`)  | String | Order Items |
|  `order_total` (Overrides `_ctotal`)  | String | Order Total |
|  `order_shipping` (Overrides `_cship`)  | String | Order Shipping |
|  `order_currency` (Overrides `_ccurrency`)  | String | Order Currency |

### Event Triggers
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `general` | General |
| `category` | Category |
| `product` | Product |
| `basket` | Basket |
| `checkout` | Checkout |

### Event-specific Parameters
To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `general` | General |
| `category` | Category|
| `product` | Product |
| `basket` | Basket |
| `checkout` | Checkout |

    