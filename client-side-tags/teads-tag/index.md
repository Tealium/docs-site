---
title: Teads Tag Setup Guide
description: This article describes how to set up the Teads tag.
url: https://docs.tealium.com/client-side-tags/teads-tag/
---
## Tag Tips

* Use mapping to override standard configuration values and set additional options.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Teads tag (Learn more about [how to add a tag]()).

After adding the tag, configure the following settings:

* **pid**
  * Your Teads-supplied PID

* **lang**
  * Language.
  * Default value is English ( `en`).

* **Slot**
  * The selector for placing the Ad.
  * Example: `.article .article_body &amp;gt; p`

* **Format**
* **minSlot**
* **Mobile**
* **css**

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable   | Description               |
|:-----------|:--------------------------|
| Pid        |                           |
| Lang       |                           |
| Slot       |                           |
| Format     |                           |
| minSlot    |                           |
| mobile     | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
| Skip delay |                           |
| Mute delay |                           |
| CSS        |                           |
| BTF        | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
| Mutable    | &lt;ul&gt;&lt;li&gt;Boolean&lt;/li&gt;&lt;/ul&gt; |
| AdBreaks   |                           |
| avoidSlot  |                           |
