---
title: AdRoll Smart Pixel Tag Setup Guide (Deprecated)
description: This article describes how to set up the AdRoll Smart Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adroll-smart-pixel-tag/
---

<blockquote>
This connector is now deprecated and no longer available in the tag marketplace. For the current connector, see the [Adroll Pixel tag setup guide](https://docs.tealium.com/adroll-pixel-tag/).
</blockquote>


## Tag Tips

* After initial page load, subsequent calls are made by the `adroll_record_user` function with data from the `adroll_record_user` object in mapping.
* To add the `name=param`, map a value to `adroll_segments` using mapping toolbox. Ssample values are `checkout` or `orderconfirm`.
* Use mapping to set `adroll_custom_data` values, such as map `_corder` to `adroll_custom_data.ORDER_ID`.
* The `adroll_conversion_value` is automatically mapped to `_csubtototal` from E-Commerce Extension
* The `adroll_conversion_value` parameter will only be set if an Order ID is set.

## Tag Configuration

First, go to Tealium's tag marketplace and add the AdRoll Smart Pixel tag (Learn more about [how to add a tag](https://docs.tealium.com/manage-tags/)).

After adding the tag, configure the following settings:

* **Advertiser ID**
  * This is typically twenty-two alphanumeric characters.

* **Pixel ID**
  * This is typically twenty-two alphanumeric characters.

## Data Mappings

Mapping is the process of sending data from a [data layer variable](https://docs.tealium.com/data-layer-variables/) to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](https://docs.tealium.com/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`adroll_custom_data.myvar`|  <ul><li>Custom Data</li></ul> |
|`adroll_record_user.myvar`|  <ul><li>Custom Record User Data</li></ul> |
|`adroll_conversion_value`|  <ul><li>Conversion Value</li></ul> |
|`adroll_currency`|  <ul><li>Currency</li></ul> |
|`adroll_segments`|  <ul><li>Segments</li></ul> |
|`adroll_email`|  <ul><li>Email</li></ul> |
|`adroll_custom_data.product_id`|  <ul><li>Product ID</li></ul> |
|`adroll_custom_data.product_group`|  <ul><li>Product Group</li></ul> |
|`adroll_custom_data.product_action`|  <ul><li>Product Action</li></ul> |
|`adroll_custom_data.product_category_id`|  <ul><li>Product Category</li></ul> |
|`adroll_adv_id`|  <ul><li>Adv Id</li></ul> |
|`adroll_pix_id`|  <ul><li>Pix Id</li></ul> |
