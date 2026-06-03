---
title: Hotjar Tag Setup Guide
description: This article describes how to configure the Hotjar Tag.
url: https://docs.tealium.com/client-side-tags/hotjar-tag/
---
## Tag Tips

Use mapping to dynamically override the standard config values.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Hotjar tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **Hotjar ID**
  * Your Hotjar Site ID.

* **Hotjar Snippet Version**
  * The version of your tracking code from Hotjar.

### Add Tag from Code (Optional)

Use the following steps to add the Hotjar tag from code&#34;

1. Log in to your Hotjar account.
1. From the account dashboard, click **Install code manually**.
1. Click **Copy to clipboard**.
1. Log in to Tealium iQ Tag Management, go to **iQ Tag Management &amp;gt; Tags**.
1. Click **Add Tag**.
1. Click **Detect Tag from Code**.
1. Paste the code you copied in Step 3.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

|Variable| Description|
|---| ---|
|`hjid`|  &lt;ul&gt;&lt;li&gt;Hotjar ID&lt;/li&gt;&lt;/ul&gt; |
| `hjsv` |  &lt;ul&gt;&lt;li&gt;Hotjar Snippet Version&lt;/li&gt;&lt;/ul&gt; |
