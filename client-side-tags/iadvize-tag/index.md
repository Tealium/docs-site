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

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Site ID**
  * Your iAdvize Site ID.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`sid`|  &lt;ul&gt;&lt;li&gt;Site ID&lt;/li&gt;&lt;/ul&gt; |
|`lang`|  &lt;ul&gt;&lt;li&gt;Language&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order/Transaction ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Sub Total/Cart Amount.&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
