---
title: Pixibo Conversion Tag Setup Guide
description: This article describes how to set up the pixibo.conversion tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/pixibo-conversion-tag/
---## Tag tips

* Use mappings to:
  * Dynamically override the standard config value for Client ID
  * Dynamically override Order and Product Details values
* Supported E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * Currency (`_ccurrency`)
  * Customer ID (`_ccusti` )
  * List of SKUs (`_csku`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Client ID**

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`clientId`|  <ul><li>String</li><li>Client ID</li></ul> |
|`size`|  <ul><li>Array</li><li>List of Product Sizes</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>(Required) Order ID</li><li>Overrides `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Sub Total</li><li>Overrides `_csubtotal`.</li></ul> |
|`order_currency`|  <ul><li>Currency</li><li>Overrides `_ccurrency`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID</li><li>Overrides `_ccustid`.</li></ul> |
|`product_sku`|  <ul><li>Array</li><li>List of SKUs</li><li>Overrides `_csku`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices</li><li>Overrides `_cprice`.</li></ul> |
