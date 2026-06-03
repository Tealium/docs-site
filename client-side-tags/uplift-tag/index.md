---
title: Uplift Tag Setup Guide
description: This article describes how to set up the UpLift tag in your Tealium iQ Tag Management account.
url: https://docs.tealium.com/client-side-tags/uplift-tag/
---## Tag tips

* Use mapping to dynamically override the standard configuration values.
* The Domain configuration has been deprecated.

### Tag configuration

Go to the tag marketplace to add a new tag. For more information about how to add a tag, see [Manage tags]().

When adding the tag, configure the following settings:

* **UP Code**
  * The UP Code (Account ID) provided by your Uplift contact.
* **Domain**
  * The domain of the host site. (Deprecated)

## Data mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`acct`|  &lt;ul&gt;&lt;li&gt;UP Code&lt;/li&gt;&lt;/ul&gt; |
|`domain`|  &lt;ul&gt;&lt;li&gt;Domain&lt;/li&gt;&lt;li&gt;Deprecated&lt;/li&gt;&lt;/ul&gt; |
