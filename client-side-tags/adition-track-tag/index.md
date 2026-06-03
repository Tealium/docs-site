---
title: Adition (Track) Tag Setup Guide
description: This article describes how to set up the Adition (Track) tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/adition-track-tag/
---
## Tag Tips

* This is the Track version of Adition.
* Set the domain according to your agreement with Adition.

  * Default value: `adfarm1.adition.com`
  * AdfarmID: `ad&lt;id&gt;.adfarm1.adition.com`
  * Custom: `&lt;subdomain&gt;.&lt;domain&gt;.&lt;tld&gt;`

* The default return type is `img`.
* Uses the following E-Commerce Variables

  * `_cprod`
  * `_cquan`
  * `_cprice`
  * `_corder`

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Adition (Track) tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Domain**
  * Domain supplied by Adition.
  * Default domain is `adfarm1.adition.com`.

* **TID**
  * (Required) Represents the landing page within the Adition ad serving system.

* **SID**
  * (Required) Represents the tracking spot within the Adition ad serving system.

* **Tag Type**:

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|Tag Type|  &lt;ul&gt;&lt;li&gt;Tag Type&lt;/li&gt;&lt;/ul&gt; |
|Domain|  &lt;ul&gt;&lt;li&gt;Domain&lt;/li&gt;&lt;/ul&gt; |
| `tid` |  &lt;ul&gt;&lt;li&gt;Landing Page ID&lt;/li&gt;&lt;/ul&gt; |
| `sid` |  &lt;ul&gt;&lt;li&gt;Tracking Spot ID&lt;/li&gt;&lt;/ul&gt; |
|`orderid`|  &lt;ul&gt;&lt;li&gt;Order ID&lt;/li&gt;&lt;li&gt;Overrides `_corder` .&lt;/li&gt;&lt;/ul&gt; |
|`descr`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Item description.&lt;/li&gt;&lt;li&gt;Overrides `_cprod` .&lt;/li&gt;&lt;/ul&gt; |
| `quantity` |  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Item quantity.&lt;/li&gt;&lt;li&gt;Overrides `_cquan` .&lt;/li&gt;&lt;/ul&gt; |
|`price`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Item price.&lt;/li&gt;&lt;li&gt;Overrides `_cprice` .&lt;/li&gt;&lt;/ul&gt; |
|`total`|  &lt;ul&gt;&lt;li&gt;Array&lt;/li&gt;&lt;li&gt;Total price.&lt;/li&gt;&lt;/ul&gt; |
|`param`|  &lt;ul&gt;&lt;li&gt;Param&lt;/li&gt;&lt;li&gt;Values are 1 - 20.&lt;/li&gt;&lt;/ul&gt; |
