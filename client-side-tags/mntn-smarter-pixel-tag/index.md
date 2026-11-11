---
title: MNTN Smarter Pixel Tag Setup Guide
description: This article describes how to set up the MNTN (formerly Steelhouse) Smarter Pixel tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/mntn-smarter-pixel-tag/
---

## Tag tips

* Use mapping to dynamically override the Account ID or to pass data into the `additional` parameter.
* Conversion tag fires when the Order ID is set.
* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * List of Product IDs (`_cprod`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**
  * For example, `12345`

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`acct`| Account ID|

### Additional Variables

|Variable| Description|
|---| ---|
|`adv.track.myvar`|  Additional Tracking Variable |
|`adv.conv.myvar`|  Account Conversion Variable |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID</li><li>Overrides `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Subtotal</li><li>Overrides `_csubtotal`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs.</li><li>Overrides `_cprod`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices.</li><li>Overrides `_cprice`</li></ul> |
