---
title: Teads Advertiser Tag Setup Guide
description: This article describes how to set up the Teads Advertiser tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/teads-advertiser-tag/
---
## Tag Tips

* Use mappings to override or dynamically set the tag configurations.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Teads Advertiser Tag tag (Learn more about [how to add a tag]()).

After adding the tag, configure the settings in the Data Mapping section.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable         | Description                                                                                      |
|:-----------------|:-------------------------------------------------------------------------------------------------|
| `advertiserId`   | &lt;ul&gt;&lt;li&gt;(Required) Your Teads-supplied Advertiser ID.&lt;/li&gt;&lt;li&gt;Example: `123456`&lt;/li&gt;&lt;/ul&gt; |
| `conversionType` | &lt;ul&gt;&lt;li&gt;(Optional) The name or type of conversion.&lt;/li&gt;&lt;/ul&gt;                              |
| `name` | Name |
| `price` | Price |
| `currency` | Currency |

