---
title: Glassbox Detector Tag Setup Guide
description: This article describes how to set up the Glassbox Detector tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/glassbox-detector-tag/
---## Tag tips

* Use mappings to override or dynamically set the tag configurations.

## Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().


## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`src_link`|  &lt;ul&gt;&lt;li&gt;Source Link&lt;/li&gt;&lt;li&gt;Link to Glassbox JavaScript&lt;/li&gt;&lt;/ul&gt; |
|`data-clsconfig`|  &lt;ul&gt;&lt;li&gt;`data-clsconfig` must contain `reportURI`.&lt;/li&gt;&lt;li&gt;Can also include additional optional parameters.&lt;/li&gt;&lt;/ul&gt; |
