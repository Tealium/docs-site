---
title: Pepperjam Tag Setup Guide
description: This article describes how to set up the Pepperjam tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pepperjam-tag/
---## Tag tips

* Supports the following E-Commerce extension values:
  * Order ID
  * Sub Total
  * Promo Code
  * List of Product IDs
  * List of Prices
  * List of Quantities
  * List of Categories
* The "Standard Integration Type" value only applies when the tag integration value is "Standard".

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Program ID**  
Your ID provided to you by Pepperjam.
* **Integration**
* **Standard Integration Type**  
This selection only affects the Standard integration of this tag.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`base_url`|  <ul><li>Base URL</li></ul> |
|`pid`|  <ul><li>Program ID</li></ul> |
|`integration`|  <ul><li>Integration</li><li>Values are:  <ul><li>STANDARD</li><li>DYNAMIC</li><li>ITEMIZED</li></ul> </li></ul> |
|`type`|  <ul><li>Standard Integration Type</li><li>Values are **1** or **2**.</li></ul> |
|`new_to_file`|  <ul><li>New to FIle</li><li>Values are  or **1**.</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID</li><li>Overrides `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Subtotal</li><li>Overrides `_csubtotal`.</li></ul> |
|`order_coupon_code`|  <ul><li>Promo Code</li><li>Overrides `_cpromo`.</li></ul> |
|`product_id`|  <ul><li>Array</li><li>List of Product IDs</li><li>Overrides `_cprod`.</li></ul> |
|`product_category`|  <ul><li>Array</li><li>List of Categories</li><li>Overrides `_ccat`.</li></ul> |
|`product_quantity`|  <ul><li>Array</li><li>List of Quantities</li><li>Overrides `_cquan`.</li></ul> |
|`product_unit_price`|  <ul><li>Array</li><li>List of Prices</li><li>Overrides `_cprice`.</li></ul> |
