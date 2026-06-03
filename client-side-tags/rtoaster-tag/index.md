---
title: RToaster Tag Setup Guide
description: This article describes how to set up the RToaster tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/rtoaster-tag/
---
## Tag Tips

* You can configure more than one element ID by entering the IDs as a comma-separated list.
* Use mappings to override standard config values.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Rtoaster tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Account ID**
  * Your Rtoaster Account ID.

* **Recommendation Element ID**
  * The IDs of the elements targeted by the Rtoaster recommendation.
  * You can enter more than one ID in a comma-separated list.

* **Popup Element ID**
  * The ID of the element targeted by the Rtoaster popup recommendation.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`account_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Account ID&lt;/li&gt;&lt;/ul&gt; |
|`element_id`|  &lt;ul&gt;&lt;li&gt;String, Array&lt;/li&gt;&lt;li&gt;Element ID&lt;/li&gt;&lt;/ul&gt; |
|`popup_element_id`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Popup Element ID&lt;/li&gt;&lt;/ul&gt; |
|`category`|  &lt;ul&gt;&lt;li&gt;String, Array&lt;/li&gt;&lt;li&gt;Category&lt;/li&gt;&lt;/ul&gt; |
|`price_min`|  &lt;ul&gt;&lt;li&gt;String, Number&lt;/li&gt;&lt;li&gt;Price Minimum&lt;/li&gt;&lt;/ul&gt; |
|`price_max`|  &lt;ul&gt;&lt;li&gt;String, Number&lt;/li&gt;&lt;li&gt;Price Maximum&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Subtotal&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`order_shipping`|  &lt;ul&gt;&lt;li&gt;Shipping amount.&lt;/li&gt;&lt;li&gt;Overrides `_cship`.&lt;/li&gt;&lt;/ul&gt; |
|`customer_id`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;li&gt;Overrides `_ccustid`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |
