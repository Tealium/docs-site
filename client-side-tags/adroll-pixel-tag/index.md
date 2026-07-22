---
title: AdRoll Pixel Tag Setup Guide
description: This article describes how to set up the AdRoll Pixel tag.
url: https://docs.tealium.com/client-side-tags/adroll-pixel-tag/
---
AdRoll provides a single platform for ecommerce brands to easily launch display ads, social media ads, and email that engages existing customers, attracts new customers, and grows revenue.

## Tag tips

* Supports the E-Commerce extension for:
  * Subtotal/Conversion Value
  * Order Currency/Conversion Currency
  * Order ID/Transaction ID
  * List of Product IDs
  * List of Categories
  * List of Quantities
  * List of Prices
* Use mapping to dynamically override the standard configuration values and the E-Commerce extension values.
* Purchase tracking occurs automatically when an order ID is populated.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Advertiser ID**: The Adroll advertiser ID (`adroll_adv_id`).
* **Pixel ID**: The Adroll pixel ID (`adroll_pix_id`).

## Load rules

Load the tag on all pages or set conditions for when your tag will load. For more information, see [About load rules](https://docs.tealium.com/about-load-rules/).

## Data mappings

Mapping is the process of sending data from a data layer variable to the corresponding destination variable of the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag Configuration

| Variable | Type |Description |
|:---------|---|:------------|
|`adroll_adv_id`  | String | Advertiser ID |
|`adroll_pix_id`  | String |  Pixel ID |

### Standard

| Variable | Type | Description |
|:---------|---| :------------|
| `total`  | String |Total |
| `cartValue`  | String |Cart value |
| `product_group`  | String | Product group |
|`site_type`  | String |  Site type |
| `keywords`  | String | Keywords |

### E-Commerce

| Variable | Data Type | Description                            |
|:----------|:----------|:---------------------------------------|
| `conversion_value` | String    | Order subtotal/Conversion value (Overrides `_csubtotal`) |
| `currency` | String    | Order currency/Conversion currency (Overrides `_ccurrency`) |
| `order_id` | String    | Order ID/Transaction ID (Overrides `_corder`) |
| `product_id` | Array     | Product IDs (Overrides `_cprod`) |
| `category` | Array     | Product categories (Overrides `_ccat`) |
| `quantity`| Array     | Product quantities (Overrides `_cquan`) |
| `price` | Array     | Product prices (Overrides `_cprice`) |



### Events

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable | Description |
|:------------|:---------|
| `productView` | Product view |
| `homeView` | Home view |
| `productSearch` | Product search |
| `addToCart` | Add to cart |
| `purchase` | Purchase |
| `pageView` | Page view |
| `custom` | Custom |


### Event-specific Parameters

To map events, refer to [Create an Event Mapping](https://docs.tealium.com/iq-tag-management/data-mappings/manage/#add-an-event-mapping)

| Variable   | Description |
|:-----------|:------------|
| `productView` | Product view |
| `homeView`    | Home view    |
| `productSearch` | Product search |
| `addToCart`  | Add to cart   |
| `purchase`   | Purchase      |
| `pageView`   | Page view     |
| `custom`     | Custom        |

