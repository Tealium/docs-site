---
title: Pixibo FYF Tag Setup Guide
description: This article describes how to set up the "Find your Fit" pixibo.fyf tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/pixibo-fyf-tag/
---## Tag tips

* Use mappings to dynamically override the standard config values.
* SKU ID in mapping is required for the tag to fire.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **Client Name**
* **Client ID**
* **Environment**
  * Used to specify the environment of the script.
* **Language**
  * Optional
  * Language in which to load the widget.
  * The default value is English (`en`).

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`clientName`|  &lt;ul&gt;&lt;li&gt;Client Name&lt;/li&gt;&lt;/ul&gt; |
|`clientId`|  &lt;ul&gt;&lt;li&gt;Client ID&lt;/li&gt;&lt;/ul&gt; |
|`environment`|  &lt;ul&gt;&lt;li&gt;Environment&lt;/li&gt;&lt;/ul&gt; |
|`skuId`|  &lt;ul&gt;&lt;li&gt;SKU ID&lt;/li&gt;&lt;/ul&gt; |
|`lang`|  &lt;ul&gt;&lt;li&gt;Language&lt;/li&gt;&lt;/ul&gt; |
