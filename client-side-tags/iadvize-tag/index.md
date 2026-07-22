---
title: iAdvize Tag Setup Guide
description: This article describes how to set up the iAdvize tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/iadvize-tag/
---## Tag tips

* Transaction tracking occurs automatically when order ID and cart amount are populated.
* Supports the following e-commerce extension parameters:
  * Order ID (`_corder`)
  * Order Sub Total (`_csubtotal`)
* If you want to pass additional parameters in the CustomData tag, add a custom destination in the mappings toolbox.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Site ID**
  * Your iAdvize Site ID.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`sid`|  <ul><li>Site ID</li></ul> |
|`lang`|  <ul><li>Language</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order/Transaction ID.</li><li>Overrides `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Sub Total/Cart Amount.</li><li>Overrides `_csubtotal`.</li></ul> |
