---
title: Clicktale Carmel Tag Setup Guide
description: This article describes how to set up the Clicktale Carmel tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/clicktale-carmel-tag/
---## Tag tips

* Override the standard config values using mappings.
* To pass audiences and badges to Clicktale:
  * Contact your Clicktale representative to enable the receiving of this data.
  * When mapping a badge, enter the name as it should appear in Clicktale.
  * Set **Send All Audiences** to `True` to send all audiences to Clicktale in the following format:  
`window.ClicktaleEventHandler([&#34;Tealium Audience: AUDIENCE NAME&#34;, ...]);`
* Set **Send Replay Link** to `True` to make your Clicktale replay link available as the server-side attribute `clicktale_replay_link`.
* Contact your Clicktale representative to enable the generation of the replay link.
* Server-side attributes will appear in the current account and profile.
* Use a mapping to override `tealium_profile` .

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Title**
  * (Required) Identifies the tag instance.
  * Clicktale Carmel is the default name.
  * When using multiple tags by the same vendor, assign a unique name
* **Partition**
  * The partition where data is sent.
  * Example: **www07**
* **Project GUID / PTC ID**
  * Clicktale Project GUID
  * Example: **11111111-1111-1111-1111-11111111111**
* **Send Replay Link**
  * Select **True** to make your Clicktale Replay Link available as a server-side attribute.
* **Send All Audiences**
  * Select **True** to send each audience to Clicktale in the format window.
  * Example: `ClicktaleEventHandler([&#34;Tealium Audience: AUDIENCE NAME&#34;, ...]);.`
* **Send Events to ClickTale**
  * Select **True** to send Event Data to Clicktale.

## Applying load rules

[Load Rules]() determine when and where to load an instance of this tag. The &#39;Load on All Pages&#39; rule is the default load rule. To load this tag on a specific page, create a new load rule with the relevant conditions.

* Load this Tag on the page where you want to track the visitor&#39;s mouse movements.
* We recommend that this tag loads after the page has rendered completely.

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`partition`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Partition.&lt;/li&gt;&lt;li&gt;The partition where data is sent.&lt;/li&gt;&lt;li&gt;Map to this variable to dynamically configure the server partition value.&lt;/li&gt;&lt;/ul&gt; |
|`project_guid`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Project GUID.&lt;/li&gt;&lt;li&gt;Map to this variable to set the project guide field.&lt;/li&gt;&lt;/ul&gt; |
|`send_replay_link`|  &lt;ul&gt;&lt;li&gt;String, Boolean&lt;/li&gt;&lt;li&gt;Send Clicktale Replay Link&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`send_audiences`|  &lt;ul&gt;&lt;li&gt;String, Boolean&lt;/li&gt;&lt;li&gt;Send all audiences.&lt;/li&gt;&lt;li&gt;Values are **true** or **false**.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_account`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Tealium Account.&lt;/li&gt;&lt;/ul&gt; |
|`tealium_profile`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Tealium Profile.&lt;/li&gt;&lt;/ul&gt; |
|`SendEventsToClicktale`|  &lt;ul&gt;&lt;li&gt;String&lt;/li&gt;&lt;li&gt;Toggle on to Send Events to Clicktale&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [How to request an integration](https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186 &#34;https://uxanalyser.zendesk.com/hc/en-gb/articles/4405613239186&#34;)
* [Live Signals Implementation](https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals &#34;https://uxanalyser.zendesk.com/hc/en-gb/articles/4409749139346-Live-Signals&#34;)
* [Tealium Integration](http://wiki.clicktale.com/Article/Tealium_Integration)
* [Frequently Asked Questions](http://wiki.clicktale.com/Article/Frequently_asked_questions)
