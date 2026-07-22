---
title: MNTN Smarter Pixel Tag Setup Guide
description: This article describes how to set up the MNTN (formerly Steelhouse) Smarter Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/mntn-smarter-pixel-tag/
---

## Tag Tips

* Use mapping to dynamically override the Account ID or to pass data into the `additional` parameter.
* Conversion tag fires when the Order ID is set.
* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * List of Product IDs (`_cprod`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag Configuration

First, go to the tag marketplace and add the MNTN Smarter Pixel tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Account ID**
  * For example, `12345`

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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
