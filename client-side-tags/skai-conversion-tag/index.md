---
title: Skai Conversion Tag Setup Guide
description: This article describes how to set up the Skai Conversion tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/skai-conversion-tag/
---
## Tag tips

* Uses E-commerce extension (`_corder`, `_csubtotal`, `_cpromo`, `_ccurrency`).
* Order ID, Amount, Promotion Code, and Currency are automatically set. These values can be over-written by creating mappings.
* Map a value to `type` to set a dynamic Conversion Type.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags](https://docs.tealium.com/manage-tags/).

When adding the tag, configure the following settings:

* **Skai ID**
  * Refers to the subdomain of the URL.
  * Value is `00` for the following example: `//00.xg4ken.com/`
* **Profile Token**
  * Refers to the long alphanumeric value applied to the `cid` querystring parameter of the URL.
* **Conversion Type**
  * This value details the conversion type, which by default should be set to `conv`.
  * You can change this to any other relevant conversion type in your site. For example, if you want to track registrations, change it to `reg` or for lead to `lead`.

## Data mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| (`type`)|Conversion type|
| (`val`)|Order amount|
| (`orderId`)|Order ID|
| (`promoCode`)|Order promo code|
| (`valueCurrency`)|Order currency|

### Vendor Documentation

* [Skai Guide Series](https://skai.io/reports-and-whitepapers/)
