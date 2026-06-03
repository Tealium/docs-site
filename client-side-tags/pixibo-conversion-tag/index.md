---
title: Pixibo Conversion Tag Setup Guide
description: This article describes how to set up the pixibo.conversion tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pixibo-conversion-tag/
---## Tag tips

* Use mappings to:
  * Dynamically override the standard config value for Client ID
  * Dynamically override Order and Product Details values
* Supported E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * Currency (`_ccurrency`)
  * Customer ID (`_ccusti` )
  * List of SKUs (`_csku`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Client ID**

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`clientId`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Client ID&lt;/li&gt;&lt;/ul&gt; |
|`size`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product Sizes&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;(Required) Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub Total&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_currency`|  &lt;ul&gt;&lt;li&gt;Currency&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`product_sku`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of SKUs&lt;/li&gt;&lt;li&gt;Overrides `_csku`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
