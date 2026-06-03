---
title: Quora Tag Setup Guide
description: This article describes how to set up the Quora tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/quora-tag/
---
## Tag Tips

* Use mappings to:
  * Override standard configuration values
  * Set up event triggers

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Quora tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* `pixel_id`
A Quora-provided alphanumeric string uniquely identifying the pixel

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable   | Description                      |
|:-----------|:---------------------------------|
| `pixel_id` | &lt;ul&gt;&lt;li&gt;Quora Pixel ID&lt;/li&gt;&lt;/ul&gt; |

### Events

| Variable               | Description                                      |
|:-----------------------|:-------------------------------------------------|
| `ViewContent`          | &lt;ul&gt;&lt;li&gt;Page View&lt;/li&gt;&lt;li&gt;View content&lt;/li&gt;&lt;/ul&gt; |
| `Generic`              | &lt;ul&gt;&lt;li&gt;Generic&lt;/li&gt;&lt;/ul&gt;                        |
| `Purchase`             | &lt;ul&gt;&lt;li&gt;Purchase&lt;/li&gt;&lt;/ul&gt;                       |
| `GenerateLead`         | &lt;ul&gt;&lt;li&gt;Generate lead&lt;/li&gt;&lt;/ul&gt;                  |
| `CompleteRegistration` | &lt;ul&gt;&lt;li&gt;Complete registration&lt;/li&gt;&lt;/ul&gt;          |
| `AddPaymentInfo`       | &lt;ul&gt;&lt;li&gt;Add payment Information&lt;/li&gt;&lt;/ul&gt;        |
| `AddToCart`            | &lt;ul&gt;&lt;li&gt;Add to cart&lt;/li&gt;&lt;/ul&gt;                    |
| `AddToWishlist`        | &lt;ul&gt;&lt;li&gt;Add to wish list&lt;/li&gt;&lt;/ul&gt;               |
| `InitiateCheckout`     | &lt;ul&gt;&lt;li&gt;Initiate checkout&lt;/li&gt;&lt;/ul&gt;              |
| `Search`               | &lt;ul&gt;&lt;li&gt;Search&lt;/li&gt;&lt;/ul&gt;                         |
| `Custom`               | &lt;ul&gt;&lt;li&gt;Custom&lt;/li&gt;&lt;/ul&gt;                         |
