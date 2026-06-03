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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Tag configurations

|Variable| Description|
|---| ---|
|`base_url`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Base URL&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_value`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Order Value.&lt;/li&gt;&lt;li&gt;Overrides `_ctotal`.&lt;/li&gt;&lt;/ul&gt; |
|`currency`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Currency.&lt;/li&gt;&lt;li&gt;Overrides `_ccurrency`.&lt;/li&gt;&lt;/ul&gt; |
|`sku`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of SKUs.&lt;/li&gt;&lt;li&gt;Overrides `_csku`.&lt;/li&gt;&lt;/ul&gt; |
|`quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice` . &lt;/li&gt;&lt;/ul&gt; |
