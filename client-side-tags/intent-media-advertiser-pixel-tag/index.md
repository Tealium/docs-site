---
title: Intent Media Advertiser Pixel Tag Setup Guide
description: This article describes how to set up the Intent Media Advertiser Pixel tag in your Tealium iQ Tag Management (TiQ) account.
url: https://docs.tealium.com/client-side-tags/intent-media-advertiser-pixel-tag/
---## Tag tips

* Uses the following E-Commerce variables
  * `_corder`
  * `_csubtotal`/`_ctotal`
  * `_ccurrency`
  * `_ccustid`
* Page View Type / Page Category can be overridden with mappings

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Entity ID**
  * Set by Intent Media Advertiser Pixel.
* **Page View Type**
  * Must be one of: &#39;HOME&#39;, &#39;LIST&#39;, &#39;DETAILS&#39;, &#39;CART&#39;, &#39;EMAIL&#39;, &#39;EMAIL_CONFIRMATION&#39;, &#39;CONVERSION&#39;, &#39;UNKNOWN&#39;.
* **Product Category**
  * Must be one of: &#39;HOME&#39;, &#39;FLIGHTS&#39;, &#39;CARS&#39;, &#39;HOTELS&#39;, &#39;PACKAGE&#39;, &#39;EMAIL&#39;, &#39;UNKNOWN&#39;.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`Entity` ID|  &lt;ul&gt;&lt;li&gt;The entity ID.&lt;/li&gt;&lt;li&gt;Set by Intent Media Advertiser Pixel.&lt;/li&gt;&lt;/ul&gt; |
|`page_view_type`|  &lt;ul&gt;&lt;li&gt;Page View Type.&lt;/li&gt;&lt;li&gt;Must be one of the following:  &lt;ul&gt;&lt;li&gt;HOME&lt;/li&gt;&lt;li&gt;LIST&lt;/li&gt;&lt;li&gt;DETAILS&lt;/li&gt;&lt;li&gt;CART&lt;/li&gt;&lt;li&gt;EMAIL&lt;/li&gt;&lt;li&gt;EMAIL\_CONFIRMATION&lt;/li&gt;&lt;li&gt;CONVERSION&lt;/li&gt;&lt;li&gt;UNKNOWN&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;The product category.&lt;/li&gt;&lt;li&gt;Must be one of the following:  &lt;ul&gt;&lt;li&gt;HOME&lt;/li&gt;&lt;li&gt;FLIGHTS&lt;/li&gt;&lt;li&gt;CARS&lt;/li&gt;&lt;li&gt;HOTELS&lt;/li&gt;&lt;li&gt;PACKAGE&lt;/li&gt;&lt;li&gt;EMAIL&lt;/li&gt;&lt;li&gt;UNKNOWN&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`page_id`|  &lt;ul&gt;&lt;li&gt;Page ID&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides Default `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Order subtotal.&lt;/li&gt;&lt;li&gt;(Overrides Default `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`currency`|  &lt;ul&gt;&lt;li&gt;Currency.&lt;/li&gt;&lt;li&gt;Overrides Default `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`custid`|  &lt;ul&gt;&lt;li&gt;Customer ID.&lt;/li&gt;&lt;li&gt;Overrides Default `_ccustid` ( `user_member_id`).&lt;/li&gt;&lt;/ul&gt; |
