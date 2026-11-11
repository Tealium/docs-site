---
title: Connexity Pixel Setup Guide
description: This article describes how to set up the Connexity Pixel tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/connexity-pixel/
---

Connexity is a performance marketing technology company whose core purpose is to help online retailers find new customers and drive sales at a cost that meets ROAS objectives.

## Tag tips

* Use mappings to:
  * Dynamically override configuration data
  * Dynamically override the E-Commerce extension values
  * Send additional data values
  * Provide event-specific parameters
  * Specify an event trigger
* Supports the following E-Commerce extension values:
  * Order ID
  * Order Sub Total
  * Product Quantities
  * Currency

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Merchant ID**: Your Connexity provided Merchant ID

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`mid`|Merchant ID|
|`page_type`|Page Type| 

### E-Commerce

|Variable| Type | Description|
|---|---|---|
|`order_id` | String |Order ID (Overrides `_corder`)|
|`order_value` | String | Order Value (Overrides `csubtotal`) |
|`order_currency` | String | Currency (Overrides `_ccurrency`)|
|`category_name` | String | Category Name (Overrides `ccat`)|
|`product_sku` | Array |Product SKU (Overrides `csku`)|
|`product_quantity` | Array | Product Quantities (Overrides `_cquan`)|
|`cust type` | String |Custom Type|
|`category_id`| String |Category ID|



### Event Triggers

|Variable| Description|
|---| ---|
| `pageview`|Page view|
|`conversion`|Conversion| 
| `addtocart`|Add to cart|
| `Custom Event`|Custom Event|

### Event-specific Parameters

|Variable| Description|
|---| ---|
|Page View| Page view|
|Add to Cart| Add to cart|
|Conversion| Conversion|
|Custom Event| Custom Event|
