---
title: APPRL Tag Setup Guide
description: This article describes how to set up the APPRL tag in your Tealium iQ Tag Management account.
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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

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
