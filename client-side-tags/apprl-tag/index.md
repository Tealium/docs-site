---
title: APPRL Tag Setup Guide
description: This article describes how to set up the APPRL tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/apprl-tag/
---## Tag tips

* Order tracking occurs automatically if an order ID is populated.
* Supports the following E-Commerce extension values:
  * Order ID
  * Order Total
  * Order Currency
  * List of SKUs
  * List of Quantities
  * List of Prices

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Tag configurations

|Variable| Description|
|---| ---|
|`base_url`|  <ul><li>String</li><li>Base URL</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>String</li><li>Order ID.</li><li>Overrides `_corder`.</li></ul> |
|`order_value`|  <ul><li>String</li><li>Order Value.</li><li>Overrides `_ctotal`.</li></ul> |
|`currency`|  <ul><li>String</li><li>Currency.</li><li>Overrides `_ccurrency`.</li></ul> |
|`sku`|  <ul><li>Array</li><li>List of SKUs.</li><li>Overrides `_csku`.</li></ul> |
|`quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li></ul> |
|`price`|  <ul><li>Array</li><li>List of Prices.</li><li>Overrides `_cprice` . </li></ul> |
