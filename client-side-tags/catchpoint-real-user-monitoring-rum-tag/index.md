---
title: Catchpoint Real User Monitoring (RUM) Tag Setup Guide
description: This article describes how to set up the Catchpoint Real User Monitoring tag.
url: https://docs.tealium.com/client-side-tags/catchpoint-real-user-monitoring-rum-tag/
---
## Tag Tips

* Use mappings to set Page Groups, Variations, Insight Indicators, and Tracepoints.
* Both the value and the token for Insight Indicator and Tracepoint must be mapped with populated variables to capture this data.
* Conversion fires automatically when an Order ID is present.
* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * List of Quantities (`_cquan`)

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Catchpoint Real User Monitoring (RUM) tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **REST URL**
  * The URL provided in your tag snippet.
  * Example: `g.3gl.net/jp/xxx/v3/M`

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `pageGroup_token` |  &lt;ul&gt;&lt;li&gt;Page Group Token.&lt;/li&gt;&lt;/ul&gt; |
| `variation_token` |  &lt;ul&gt;&lt;li&gt;Variation Tag Token.&lt;/li&gt;&lt;/ul&gt; |
| `indicator_token` |  &lt;ul&gt;&lt;li&gt;Indicator Tag Token.&lt;/li&gt;&lt;/ul&gt; |
| `indicator_value` |  &lt;ul&gt;&lt;li&gt;Indicator Value.&lt;/li&gt;&lt;/ul&gt; |
| `tracepoint_token` |  &lt;ul&gt;&lt;li&gt;Tracepoint Token.&lt;/li&gt;&lt;/ul&gt; |
|`tracepoint_value`|  &lt;ul&gt;&lt;li&gt;Tracepoint Value.&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
| `order_id` |  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Subtotal.&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array.&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
