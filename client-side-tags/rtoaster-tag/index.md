---
title: RToaster Tag Setup Guide
description: This article describes how to set up the RToaster tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/rtoaster-tag/
---
## Tag tips

* You can configure more than one element ID by entering the IDs as a comma-separated list.
* Use mappings to override standard config values.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Account ID**
  * Your Rtoaster Account ID.

* **Recommendation Element ID**
  * The IDs of the elements targeted by the Rtoaster recommendation.
  * You can enter more than one ID in a comma-separated list.

* **Popup Element ID**
  * The ID of the element targeted by the Rtoaster popup recommendation.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`account_id`|  <ul><li>String</li><li>Account ID</li></ul> |
|`element_id`|  <ul><li>String, Array</li><li>Element ID</li></ul> |
|`popup_element_id`|  <ul><li>String</li><li>Popup Element ID</li></ul> |
|`category`|  <ul><li>String, Array</li><li>Category</li></ul> |
|`price_min`|  <ul><li>String, Number</li><li>Price Minimum</li></ul> |
|`price_max`|  <ul><li>String, Number</li><li>Price Maximum</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_subtotal`|  <ul><li>Subtotal</li><li>Overrides `_csubtotal`.</li></ul> |
|`order_shipping`|  <ul><li>Shipping amount.</li><li>Overrides `_cship`.</li></ul> |
|`customer_id`|  <ul><li>Customer ID</li><li>Overrides `_ccustid`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs.</li><li>Overrides `_cprod`</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities.</li><li>Overrides `_cquan`</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices</li><li>Overrides `_cprice`.</li></ul> |
