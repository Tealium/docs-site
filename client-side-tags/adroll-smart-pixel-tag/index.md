---
title: AdRoll Smart Pixel Tag Setup Guide (Deprecated)
description: This article describes how to set up the AdRoll Smart Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adroll-smart-pixel-tag/
---
This connector is now deprecated and no longer available in the tag marketplace. For the current connector, see the [Adroll Pixel tag setup guide]().

## Tag Tips

* After initial page load, subsequent calls are made by the `adroll_record_user` function with data from the `adroll_record_user` object in mapping.
* To add the `name=param`, map a value to `adroll_segments` using mapping toolbox. Ssample values are `checkout` or `orderconfirm`.
* Use mapping to set `adroll_custom_data` values, such as map `_corder` to `adroll_custom_data.ORDER_ID`.
* The `adroll_conversion_value` is automatically mapped to `_csubtototal` from E-Commerce Extension
* The `adroll_conversion_value` parameter will only be set if an Order ID is set.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the AdRoll Smart Pixel tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Advertiser ID**
  * This is typically twenty-two alphanumeric characters.

* **Pixel ID**
  * This is typically twenty-two alphanumeric characters.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`adroll_custom_data.myvar`|  &lt;ul&gt;&lt;li&gt;Custom Data&lt;/li&gt;&lt;/ul&gt; |
|`adroll_record_user.myvar`|  &lt;ul&gt;&lt;li&gt;Custom Record User Data&lt;/li&gt;&lt;/ul&gt; |
|`adroll_conversion_value`|  &lt;ul&gt;&lt;li&gt;Conversion Value&lt;/li&gt;&lt;/ul&gt; |
|`adroll_currency`|  &lt;ul&gt;&lt;li&gt;Currency&lt;/li&gt;&lt;/ul&gt; |
|`adroll_segments`|  &lt;ul&gt;&lt;li&gt;Segments&lt;/li&gt;&lt;/ul&gt; |
|`adroll_email`|  &lt;ul&gt;&lt;li&gt;Email&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_id`|  &lt;ul&gt;&lt;li&gt;Product ID&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_group`|  &lt;ul&gt;&lt;li&gt;Product Group&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_action`|  &lt;ul&gt;&lt;li&gt;Product Action&lt;/li&gt;&lt;/ul&gt; |
|`adroll_custom_data.product_category_id`|  &lt;ul&gt;&lt;li&gt;Product Category&lt;/li&gt;&lt;/ul&gt; |
|`adroll_adv_id`|  &lt;ul&gt;&lt;li&gt;Adv Id&lt;/li&gt;&lt;/ul&gt; |
|`adroll_pix_id`|  &lt;ul&gt;&lt;li&gt;Pix Id&lt;/li&gt;&lt;/ul&gt; |
