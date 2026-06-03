---
title: Alphonso Website Tag Setup Guide
description: This article describes how to set up the Alphonso Website Tag tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/alphonso-website-tag/
---## Tag tips

* The Use Default configuration options will cause the tag to act in the same manner as placing the snippet directly on your page.
* The Session ID, UTM Source, and UTM Medium populate automatically. To manage these options yourself, turn these options off.
* Add custom values by using the **&#43; Add Custom Destination** button.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Customer ID**
  * A value provided by Alphonso.
* **Use Default Session Management**
  * Use the Alphonso session management included with the code snippet.
  * If set to **no**, you will need to map Session ID.
* **Use Default UTM Parsing**
  * Use the Alphonso UTM parameter parsing included with the code snippet.
  * If set to **no**, you will need to map Campaign Source and Campaign Medium

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Description| Description|
|---| ---|
|`cust`|  &lt;ul&gt;&lt;li&gt;Customer ID&lt;/li&gt;&lt;/ul&gt; |
|`ord`|  &lt;ul&gt;&lt;li&gt;Cache Buster&lt;/li&gt;&lt;/ul&gt; |
|`utm_src`|  &lt;ul&gt;&lt;li&gt;Campaign Source&lt;/li&gt;&lt;/ul&gt; |
|`utm_mdm`|  &lt;ul&gt;&lt;li&gt;Campaign Medium&lt;/li&gt;&lt;/ul&gt; |
|`url`|  &lt;ul&gt;&lt;li&gt;Page URL&lt;/li&gt;&lt;/ul&gt; |
|`title`|  &lt;ul&gt;&lt;li&gt;Page Title&lt;/li&gt;&lt;/ul&gt; |
|`session_id`|  &lt;ul&gt;&lt;li&gt;Session ID&lt;/li&gt;&lt;/ul&gt; |
|`sess_status`|  &lt;ul&gt;&lt;li&gt;Session Status&lt;/li&gt;&lt;/ul&gt; |
|`ref`|  &lt;ul&gt;&lt;li&gt;Referrer URL&lt;/li&gt;&lt;/ul&gt; |
|`event_type`|  &lt;ul&gt;&lt;li&gt;Event Name&lt;/li&gt;&lt;/ul&gt; |
|`event_value`|  &lt;ul&gt;&lt;li&gt;Event Value&lt;/li&gt;&lt;/ul&gt; |
|`useDefaultSession`|  &lt;ul&gt;&lt;li&gt;Use Default Session Management&lt;/li&gt;&lt;/ul&gt; |
|`useDefaultUtm`|  &lt;ul&gt;&lt;li&gt;Use Default UTM Parsing&lt;/li&gt;&lt;/ul&gt; |
|`useOnBeforeUnload`|  &lt;ul&gt;&lt;li&gt;Use OnBeforeUnload Pixel&lt;/li&gt;&lt;/ul&gt; |
