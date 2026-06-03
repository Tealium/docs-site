---
title: Quantcast Easy Tag for Advertise Setup Guide
description: This article describes how to set up the Quantcast Easy Tag for Advertise in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/quantcast-easy-tag-for-advertise/
---
## Tag Tips

* Use mappings to:
  * Dynamically override the standard configuration value for account.
  * Dynamically override the E-Commerce extension values.
  * Pass any `_fp` label as part of `_qevents`.
  * Pass any freeform label (`mylabel`).
  * Mapping arrays to freeform labels will be handled according to Quantcast documentation.

* Supports the following E-Commerce extension parameters:
  * Order ID (`_corder`)
  * Order Subtotal (`_csubtotal`)

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Quantcast Easy Tag for Advertise tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Account Code**
  * Account Code (P-code).
  * A 13-character, case sensitive, alpha-numeric code that begins with `p-`.
  * Contact your Quantcast representative if you have questions.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`qacct`|  &lt;ul&gt;&lt;li&gt;Account Code (P-code).&lt;/li&gt;&lt;li&gt;A 13-character, case sensitive, alpha-numeric code that begins with `p-`.&lt;/li&gt;&lt;/ul&gt; |
|`_fp.event`|  &lt;ul&gt;&lt;li&gt;Event&lt;/li&gt;&lt;/ul&gt; |
|`_fp.channel`|  &lt;ul&gt;&lt;li&gt;Channel&lt;/li&gt;&lt;/ul&gt; |
|`_fp.subchannel`|  &lt;ul&gt;&lt;li&gt;Subchannel&lt;/li&gt;&lt;/ul&gt; |
|`_fp.customer`|  &lt;ul&gt;&lt;li&gt;Customer&lt;/li&gt;&lt;/ul&gt; |
|`_fp.pcat`|  &lt;ul&gt;&lt;li&gt;Product Category&lt;/li&gt;&lt;/ul&gt; |
|`mylabel`|  &lt;ul&gt;&lt;li&gt;Custom Label&lt;/li&gt;&lt;/ul&gt; |

### E-Commerce

|Variable| Description|
|---| ---|
|`orderid`|  &lt;ul&gt;&lt;li&gt;Order ID.&lt;/li&gt;&lt;li&gt;Overrides E-Comm Order ID.&lt;/li&gt;&lt;/ul&gt; |
|`revenue`|  &lt;ul&gt;&lt;li&gt;Revenue.&lt;/li&gt;&lt;li&gt;Overrides E-Comm Order Subtotal.&lt;/li&gt;&lt;/ul&gt; |
