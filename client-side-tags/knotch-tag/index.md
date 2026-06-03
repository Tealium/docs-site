---
title: Knotch Tag Setup Guide
description: This article describes how to configure the Knotch Tag.
url: https://docs.tealium.com/client-side-tags/knotch-tag/
---
## Tag Tips

* Minimum utag.js Version: 4.36. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* Use mapping to dynamically override the standard configuration values.

## Tag Configuration

First, go to Tealium&#39;s tag marketplace and add the Knotch tag (Learn more about [how to add a tag]()).

After adding the tag, configure the settings in the Data Mapping section.

## Data Mappings

Mapping is the process of sending data from a [data layer variable]() to the corresponding destination variable of the vendor tag. For instructions on how to map a variable to a tag destination, see [Data Mappings](/iq-tag-management/data-mappings/manage/).

The available categories are:

### Standard

| Variable          | Description                                                                                                                                  |
|:------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|
| `unit_id`         | &lt;ul&gt;&lt;li&gt;Your Knotch Unit ID.&lt;/li&gt;&lt;li&gt;For example, `knotch_12ab3cd456ef789a0bc12345`&lt;/li&gt;&lt;/ul&gt;                                                    |
| `tag_type`        | &lt;ul&gt;&lt;li&gt;Values are `js` or `iframe`&lt;/li&gt;&lt;/ul&gt;                                                                                                |
| `target_element`  | &lt;ul&gt;&lt;li&gt;The DOM ID of the element (already on the page) where the Knotch widget should appear.&lt;/li&gt;&lt;/ul&gt;                                     |
| `widget_position` | &lt;ul&gt;&lt;li&gt;The position of the Knotch widget relative to the target element.&lt;/li&gt;&lt;li&gt;Values are `append_child`, `before`, or `after`.&lt;/li&gt;&lt;/ul&gt; |
