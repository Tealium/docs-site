---
title: Amazon Ads Server Tag Setup Guide
description: This article describes how to set up the Amazon Ads Server tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/amazon-ads-server-tag/
---
## How it works

Amazon Ads Server is a single and secure tool to deploy, manage, and update digital marketing tags on a site without having to continuously update your website code.

## Tag Tips

* Supports the following E-Commerce extension values:
  * Order ID
  * List of Product IDs
  * List of Product Names
  * List of Quantities
  * List of Product Prices

* Use mapping to:
  * Dynamically override the E-Commerce extension values
  * Define the contents of the Activity Params object
    * Using `act`
  * Define the contents of the Retargeting Params object
    * Using `rtp`
  * Define the contents of the Dynamic Retargeting Params object
    * Using `drtp`
  * Define the contents of the Conditional Params object
    * Using `cp`
  * Dynamic Pages and Events
    * Set a value for url (overrides `url`)

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Amazon Ads Server tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **AAS Tag Manager ID**
  * Example: `123`

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
| `id` |  &lt;ul&gt;&lt;li&gt;VersaTag ID&lt;/li&gt;&lt;/ul&gt; |
|`url`|  &lt;ul&gt;&lt;li&gt;URL&lt;/li&gt;&lt;/ul&gt; |
|`mobile`|  &lt;ul&gt;&lt;li&gt;Mobile&lt;/li&gt;&lt;li&gt;Default value is `0`.&lt;/li&gt;&lt;/ul&gt; |
|`sync`|  &lt;ul&gt;&lt;li&gt;Sync&lt;/li&gt;&lt;li&gt;Default value is `0`.&lt;/li&gt;&lt;/ul&gt; |
|`dispType`|  &lt;ul&gt;&lt;li&gt;Display type.&lt;/li&gt;&lt;li&gt;Default value is `js`.&lt;/li&gt;&lt;/ul&gt; |
|`ActivityID`|  &lt;ul&gt;&lt;li&gt;Activity ID&lt;/li&gt;&lt;/ul&gt; |
|`Session`|  &lt;ul&gt;&lt;li&gt;Session&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`order_id`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides `_corder`.&lt;/li&gt;&lt;/ul&gt; |
|`product_id`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Product IDs.&lt;/li&gt;&lt;li&gt;Overrides `_cprod`.&lt;/li&gt;&lt;/ul&gt; |
|`product_name`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Names.&lt;/li&gt;&lt;li&gt;Overrides `_cprodname`.&lt;/li&gt;&lt;/ul&gt; |
|`product_quantity`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Quantities.&lt;/li&gt;&lt;li&gt;Overrides `_cquan`.&lt;/li&gt;&lt;/ul&gt; |
|`product_unit_price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;List of Prices.&lt;/li&gt;&lt;li&gt;Overrides `_cprice`.&lt;/li&gt;&lt;/ul&gt; |

### Configurable Parameters

|Variable| Description|
|---| ---|
|`act.###`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Activity Params.&lt;/li&gt;&lt;/ul&gt; |
|`rtp.###`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Retargeting Params.&lt;/li&gt;&lt;/ul&gt; |
|`drtp.###`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Dynamic Retargeting Params.&lt;/li&gt;&lt;/ul&gt; |
|`cp.###`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Conditional Params.&lt;/li&gt;&lt;/ul&gt; |
|`activityParams`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Activity Params.&lt;/li&gt;&lt;/ul&gt; |
|`retargetParams`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Retargeting Params.&lt;/li&gt;&lt;/ul&gt; |
|`dynamicRetargetParams`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;Dynamic Retargeting Params.&lt;/li&gt;&lt;/ul&gt; |
|`conditionalParams`|  &lt;ul&gt;&lt;li&gt;Object&lt;/li&gt;&lt;li&gt;`meta charset=&#34;utf-8&#34;`&lt;/li&gt;&lt;li&gt;Conditional Params.&lt;/li&gt;&lt;/ul&gt; |
