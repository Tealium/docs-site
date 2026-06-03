---
title: MNTN Smarter Pixel Tag Setup Guide
description: This article describes how to set up the MNTN (formerly Steelhouse) Smarter Pixel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/mntn-smarter-pixel-tag/
---

## Tag Tips

* Use mapping to dynamically override the Account ID or to pass data into the `additional` parameter.
* Conversion tag fires when the Order ID is set.
* Supports these E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Sub Total (`_csubtotal`)
  * List of Product IDs (`_cprod`)
  * List of Quantities (`_cquan`)
  * List of Prices (`_cprice`)

## Tag Configuration

First, go to the tag marketplace and add the MNTN Smarter Pixel tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Account ID**
  * For example, `12345`

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [data mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`acct`| Account ID|

### Additional Variables

|Variable| Description|
|---| ---|
|`adv.track.myvar`|  Additional Tracking Variable |
|`adv.conv.myvar`|  Account Conversion Variable |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`order_subtotal`|  &lt;ul&gt;&lt;li&gt;Subtotal&lt;/li&gt;&lt;li&gt;Overrides `_csubtotal`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`&lt;/li&gt;&lt;/ul&gt; |
