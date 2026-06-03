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
* The &#34;Standard Integration Type&#34; value only applies when the tag integration value is &#34;Standard&#34;.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Program ID**  
Your ID provided to you by Pepperjam.
* **Integration**
* **Standard Integration Type**  
This selection only affects the Standard integration of this tag.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`base_url`|  &lt;ul&gt;&lt;li&gt;Base URL&lt;/li&gt;&lt;/ul&gt; |
|`pid`|  &lt;ul&gt;&lt;li&gt;Program ID&lt;/li&gt;&lt;/ul&gt; |
|`integration`|  &lt;ul&gt;&lt;li&gt;Integration&lt;/li&gt;&lt;li&gt;Values are:  &lt;ul&gt;&lt;li&gt;STANDARD&lt;/li&gt;&lt;li&gt;DYNAMIC&lt;/li&gt;&lt;li&gt;ITEMIZED&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|`type`|  &lt;ul&gt;&lt;li&gt;Standard Integration Type&lt;/li&gt;&lt;li&gt;Values are **1** or **2**.&lt;/li&gt;&lt;/ul&gt; |
|`new_to_file`|  &lt;ul&gt;&lt;li&gt;New to FIle&lt;/li&gt;&lt;li&gt;Values are  or **1**.&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Subtotal&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_coupon_code`|  &lt;ul&gt;&lt;li&gt;Promo Code&lt;/li&gt;&lt;li&gt;Overrides `_cpromo`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_category`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Categories&lt;/li&gt;&lt;li&gt;Overrides `_ccat`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
