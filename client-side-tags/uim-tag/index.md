---
title: United Internet Media (UIM) Retargeting Tag Setup Guide
description: This article describes how to set up the United Internet Media (UIM) Retargeting tag.
url: https://docs.tealium.com/client-side-tags/uim-tag/
---
## Tag tips

* Use mappings to override or dynamically set tag configurations.
* Use mappings to trigger events.
* Supports the following E-Commerce extension parameters:
    &#43; Order ID (Overrides `_corder`)
    &#43; Order Items (Overrides `_cprod`)
    &#43; Order Total (Overrides `_ctotal`)
    &#43; Order Shipping (Overrides `_cship`)
    &#43; Order Currency (Overrides `_ccurrency`)
    &#43; Product ID (Overrides `_cprod`)
    &#43; Product Name (Overrides `_cprodname`)
    &#43; Product Price (Overrides` _cprice`)
    &#43; Product Currency (Overrides `_ccurrency`)
    &#43; Basket Total (Overrides `_ctotal`)
    &#43; Basket Items (Overrides `_cprod`)
    &#43; Basket Currency (Overrides `_ccurrency`)



## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Advertiser**: Advertiser in JS URL. Required

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules]().

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings]().

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
To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `general` | General |
| `category` | Category |
| `product` | Product |
| `basket` | Basket |
| `checkout` | Checkout |

### Event-specific Parameters
To map events, refer to [Create an Event Mapping](/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:---------|:------------|
| `general` | General |
| `category` | Category|
| `product` | Product |
| `basket` | Basket |
| `checkout` | Checkout |

    