---
title: Intent Media Advertiser Pixel Tag Setup Guide
description: This article describes how to set up the Intent Media Advertiser Pixel tag in your Tag Management account.
url: https://docs.tealium.com/client-side-tags/intent-media-advertiser-pixel-tag/
---## Tag tips

* Uses the following E-Commerce variables
  * `_corder`
  * `_csubtotal`/`_ctotal`
  * `_ccurrency`
  * `_ccustid`
* Page View Type / Page Category can be overridden with mappings

## Tag configuration

Go to the tag marketplace to add a new tag. For more information, see [About tags](https://docs.tealium.com/about-tags/).

When adding the tag, configure the following settings:

* **Entity ID**
  * Set by Intent Media Advertiser Pixel.
* **Page View Type**
  * Must be one of: 'HOME', 'LIST', 'DETAILS', 'CART', 'EMAIL', 'EMAIL_CONFIRMATION', 'CONVERSION', 'UNKNOWN'.
* **Product Category**
  * Must be one of: 'HOME', 'FLIGHTS', 'CARS', 'HOTELS', 'PACKAGE', 'EMAIL', 'UNKNOWN'.

## Data mappings

Data mappings send values from data layer variables to the corresponding variables in the vendor tag. For more information, see [About data mappings](https://docs.tealium.com/about-data-mappings/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`Entity` ID|  <ul><li>The entity ID.</li><li>Set by Intent Media Advertiser Pixel.</li></ul> |
|`page_view_type`|  <ul><li>Page View Type.</li><li>Must be one of the following:  <ul><li>HOME</li><li>LIST</li><li>DETAILS</li><li>CART</li><li>EMAIL</li><li>EMAIL\_CONFIRMATION</li><li>CONVERSION</li><li>UNKNOWN</li></ul> </li></ul> |
|`product_category`|  <ul><li>The product category.</li><li>Must be one of the following:  <ul><li>HOME</li><li>FLIGHTS</li><li>CARS</li><li>HOTELS</li><li>PACKAGE</li><li>EMAIL</li><li>UNKNOWN</li></ul> </li></ul> |
|`page_id`|  <ul><li>Page ID</li></ul> |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  <ul><li>Order ID.</li><li>Overrides Default `_corder`.</li></ul> |
|`order_subtotal`|  <ul><li>Order subtotal.</li><li>(Overrides Default `_csubtotal`.</li></ul> |
|`currency`|  <ul><li>Currency.</li><li>Overrides Default `_ccurrency`.</li></ul> |
|`custid`|  <ul><li>Customer ID.</li><li>Overrides Default `_ccustid` ( `user_member_id`).</li></ul> |
